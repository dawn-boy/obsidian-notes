## Machine Learning
the training of programs developed by allowing a computer to learn from it's experience, rather than through manually coding the individual steps

### terms
- the functional form of a model is called it's architecture
- the weights are called the parameters
- the predictions are calculated from the independent variable, which is just the data without including the labels
- the results of the model are called the prediction
- the measure of performance is called loss
- the loss not only on the predictions, but also the correct labels(a.k.a targets, dependent variable)

![[fastai-final_model.png]]

## positive feedback loop
example: 
- A _predictive policing_ model is created based on where arrests have been made in the past. In practice, this is not actually predicting crime, but rather predicting arrests, and is therefore partially simply reflecting biases in existing policing processes.
- Law enforcement officers then might use that model to decide where to focus their police activity, resulting in increased arrests in those areas.
- Data on these additional arrests would then be fed back in to retrain future versions of the model.
this is a positive feedback loop, where the more the model is used to predict crime hotspots, the more baised the future data becomes, which is then fed to the model to retrain itself making it even more baised and so on.

### simple image importing
```python
from fastbook import *

urls = search_images_ddg(search_term, max_images=count) #returns a list

dest = Path('bird.png')

if not dest.exists():
	download_url(urls[0],dest) #stores an image in dest

im = Image.open(dest)
im.to_thumb(500,500)
```

```python
from fastbook import *

searches = ['bird','forest']
path = Path('not_a_bird')

if path.exists():
	for search in searches:
		dest = (path/search)
		dest.mkdir(exist_ok=True)
		urls = search_images_ddg(f'{search} picture',max_images=200)
		download_images(dest,urls=urls)
		resize_images(dest,max_size=500,dest=dest)

# to unlink broken images
failed = verify_images(get_image_files(path))
failed.map(Path.unlink)

# making a data block
dls = DataBlock(blocks=(ImageBlock, CategoryBlock),
			   get_items=get_image_files,
			   splitter=RandomSplitter(valid_pct=0.2,seed=41),
			   get_y=parent_label,
			   item_tfms=[Resize(192,method='squish')]
			   ).dataloaders(path)
dls.show_batch(max_n=9)

#training a model
learn = vision_learner(dls,resnet18,metrics=error_rate)
learn.fine_tune(3)

learn.predict((PILImage.create(dest)))

#view interpretations
interp = ClassificationInterpretation.from_learner(learn)
interp.plot_confusion_matrix()

#to clean the dataset
from fastai.vision.widget import *
cleaner = ImageClassifierCleaner(learn)
cleaner

for idx in cleaner.delete():
	cleaner.fns[idx].unlink()
for idx,cat in cleaner.change():
	shutil.move(str(cleaner.fns[idx]),path/cat)

learn.export('model.pkl')
model = load_learner('model.pkl')

im = PILImage('image.png')
model.predict(im)
```