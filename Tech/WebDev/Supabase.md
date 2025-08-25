## Policies
They allow or restrict users to view the table values based on certain conditions. 
- A policy controls which rows a user can `SELECT`, `INSERT`, `UPDATE`, or `DELETE`.
- You define
	1. Who is allowed -> like `authenticated`, `role`, etc
	2. When they're allowed -> `using ()`
	3. Which operation -> `for SELECT`, `for UPDATE`

### Syntax
```sql
create policy "Policy Name"
on schema.table_name
as PERMISSIVE | RESTRICTIVE
for SELECT | INSERT | UPDATE | DELETE 
to role | authenticated | anon
using ( <condition> )
with check ( <condition> ) --> Only for INSERT and UPDATE only
```

### What is `PERMISSIVE` and `RESTRICTIVE`
#### 1. `PERMISSIVE` is a **OR Logic** between **Policies**
- `PERMISSIVE` is the default option in Supabase when no other options are given.
#### using `PERMISSIVE`
Policy 1: Users can read their own messages
```sql
create policy "Read own messages"
on messages
as PERMISSIVE
for SELECT
to authenticated
using (user_id = auth.uid());
```

Policy 2: Everyone can read public messages
```sql
create policy "Read public messages"
on messages
as PERMISSIVE
for SELECT
to authenticated
using (is_public = true);
```
##### Result
- if either condition is true the row is accessible.
#### 2. `RESTRICTIVE` is an AND Logic between polices
Things are much more stricter using `RESTRICTIVE` polices

using `RESTRICTIVE
Policy 1: Only approved users can see messages
```sql
create policy "Only allow approved users"
on messages
as RESTRICTIVE
for SELECT
to authenticated
using (auth.uid() in (select user_id from approved_users));
```

Policy 2: Messages must also be public
```sql
create policy "Only allow public messages"
on messages
as RESTRICTIVE
for SELECT
to authenticated
using (is_public = true);
```
##### Result
- Only if both the conditions are true the row is accessible


## Examples
### 1. To Allow a user to view their own row
```sql
create policy "Users can read their own profiles"
on public.users_table
for SELECT
to authenticated
using ( auth.uid() = id ) --> auth.uid gives the currently logged in user 
```

### 2. Allow a user to update only their own record
```sql
create policy "Users can update their own profiles"
on public.users_table
for UPDATE
to authenticated 
using ( auth.uid() = id )   --> if given id is in table
which check ( auth.uid() = id ); --> checking if the id stays the same after update.. if we don't keep this.. the user can change his id and impersonate another
```

### 3. Allow a user to read only the team they're in
```sql
create policy "Players can read their own teams"
on teams_table
for SELECT
to authenticated
using (
	exists(
		SELECT 1
		from players_table
		where players_table.id = auth.uid()
		and players_table.team_id = teams_table.id
	)
);
```