# One-Hot encoding
```python
def returnDNA(enc):
    match(enc):
        case [1,0,0,0]:
            return 'A'
        case [0,1,0,0]:
            return 'G'
        case [0,0,1,0]:
            return 'C'
        case [0,0,0,1]:
            return 'T'

# Conversion of dna to dna_encoded
dna = 'AGCTTGCAGTCGATCCGCTCGCTAGCTAG'

dna_map = {
    'A': [1,0,0,0],
    'G': [0,1,0,0],
    'C': [0,0,1,0],
    'T': [0,0,0,1]
}

dna_encoded = [dna_map[nuc] for nuc in dna]
print(dna_encoded)

# Conversion of dna_encoded back to dna
orginal_dna_list = [returnDNA(enc) for enc in dna_encoded]
original_dna = "".join(orginal_dna_list)
original_dna
```
### Efficient method with Numpy
```python
dna = "ACTG"
dna_encoded = [0, 1, 3, 2]
one_hot = np.eye(len(dna))[dna_encoded]
```
![[something-1758265756008.png]]
***
# K-mers based embedding
- a **k-mer** just means a thing made of k parThe core principle is the distributional hypothesis: "a word is characterized by the company it keeps."ts
- An **embedding** is a translation of our k-mer "words" into a meaningful numerical representation, specifically a vector of numbers.
### Methods for Creating K-mer Embeddings
#### 1. Bag-of-k-mers (Frequency Counts)
- It just focuses on each k-mer words frequency
- Ignores the context: **Loses all sequential information**. "ACG-GTA" is treated the same as "GTA-ACG".
#### 2. Word2Vec-style Embeddings (Context is Key)
- The core principle is the **distributional hypothesis**: *"a word is characterized by the company it keeps."*
- **The Idea**: A neural network slides a window across a vast amount of DNA data. It learns an embedding for each k-mer by training on a task: either predicting a central k-mer from its surrounding neighbors (**CBOW model**) or predicting the neighbors from a central k-mer (**Skip-gram model**). K-mers that frequently appear in similar contexts will end up with similar vectors.
- **Analogy**: You don't know what the word "pumpernickel" means. But if you see it in sentences like "I ate a sandwich on...", "I bought a loaf of...", and "... is a type of bread", you can infer its meaning from the surrounding words. In the same way, the model learns the "function" of a k-mer by observing its neighbors.
- **Pros**: Captures the contextual and "semantic" relationships between k-mers. The resulting vectors are dense and rich with information.
- **Cons**: Requires a large dataset to train effectively. The choice of `k` and other training parameters is critical.
#### 3. Pre-trained Genomic Models (The LLM Approach)
- directly inspired by large language models like BERT
- **The Idea**: Researchers take massive biological sequence databases (like all known genomes) and pre-train a huge model (e.g., **DNABERT**, **Nucleotide Transformer**) to understand the "language of DNA" on a very deep level. The model learns complex relationships, grammar, and long-range dependencies. We can then take this pre-trained model and fine-tune it for specific tasks, like finding genes or identifying viral sequences.
- **Analogy**: Instead of learning English by reading a few dozen books (Word2Vec), you learn by reading the entire internet (BERT). You become a true "native speaker" and can then apply that deep knowledge to specific tasks like writing a poem or a legal document.
- **Pros**: Extremely powerful. Captures complex, long-range patterns that other methods miss.
- **Cons**: Requires immense computational power to pre-train. For most users, the only practical option is to use an already-trained model.
### Code:
#### 1. Bag of k-mers
```python
from collections import Counter

dna_sequence = "ACGTACGTACGTTT"
k = 3

kmers = [dna_sequence[i:i+k] for i in range(len(dna_sequence) - k + 1)]

kmer_counts = Counter(kmers)

print(f"K-mer Frequencies:")
for kmer, count in kmer_counts.items():
    print(f"  {kmer}: {count}")
```
![[something-1758265712963.png]]
#### 2. Word2Vec
```python
# Step 1: Import the necessary library
from gensim.models import Word2Vec

# Step 2: Prepare our data
# A longer, repetitive sequence is better for showing context
dna_sequence = "AGATTACAGATTACAGATTACAGATTAC"
k = 3

# Step 3: Create the k-mer "sentences"
# First, generate the list of all overlapping k-mers
kmers = [dna_sequence[i:i+k] for i in range(len(dna_sequence) - k + 1)]

# Gensim's Word2Vec model expects a list of sentences.
# For our purpose, the entire sequence of k-mers is one long "sentence".
sentences = [kmers]

# Step 4: Train the Word2Vec model
# We'll use the Skip-gram model (sg=1)
model = Word2Vec(
    sentences=sentences,
    vector_size=10,    # The dimensionality of the embedding vectors.
    window=2,          # The context window size.
    min_count=1,       # Include all k-mers.
    sg=1               # Use the Skip-gram model.
)

# Step 5: Explore the trained model
print("Model training complete.")
print("-" * 30)

# Get the vector for a specific k-mer
target_kmer = "GAT"
vector = model.wv[target_kmer]
print(f"Vector for '{target_kmer}':\n{vector}")
print("-" * 30)


# Find the k-mers most similar to a target k-mer
print(f"K-mers most similar to '{target_kmer}':")
similar_kmers = model.wv.most_similar(target_kmer)
```
![[something-1758275999378.png]]`
***
####