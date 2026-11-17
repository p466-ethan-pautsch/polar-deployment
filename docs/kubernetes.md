The auditing change must be done in two releases. V4 first 
fills existing null created_by and last_modified_by values 
with 'unknown'. V5 is applied in a later release to add the 
NOT NULL constraints.

Doing both in the same release would be unsafe during a 
rolling upgrade because an older Catalog Service instance 
could still be running while the new schema is active. 
That older version may not write the new auditing fields, 
so the NOT NULL constraint could cause its writes to fail.