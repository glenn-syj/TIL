## Identifying Relationship Deep Dive

**Last Modified: 2024-04-01**

**Written By: @glenn-syj**

### Explanation

**Start Point**

I made an ERD(Entity Relation Diagram) for a simple relational database design of a small website with CRUD. I and my pair used ERD Cloud website for visualize a schema. When altering the primary key of one table to another as a foreign key, I found out that there was a two relationship with foreign key. The comprehension of identifying and the non-identifying relation was quite confusing.

**Tackling Curiosity**

Identifying and non-identifying relation is differentiated from each other in that the former uses a foreign key as a primary key and the latter not a primary key. I will start with my own miscomprehension and the notion of the exsitence dependency.

1. Exsitence Dependency

At first, I grasped the structural importance between them as a "possessing" relationship which has a higher owner and a lower posession. For exmaple, a video in the webpage owns review(s). When it is deleted, the reviews were thought to be removed either. This kind of comprehension seems to be valid, however it does not.

The real world example helps understanding the notion of the existene dependency. Assume that a specific person and his/her properties exist. When a person is gone, then should the properties be gone either? The answer is no. The properties stands in the world without its owner. Thus, recognizing the identifying relationship as a "possessing" relationship makes misunderstandings.

Rather the identifying relationship would be valid only if the sub relations should be removed through `CASCADE` keyword. Identifying relationship here could be said in another way that the entitiy is in the existence dependency. It also means that the identifying relationship needs that the foreign key should never be changed as it is immutable. Remembering that the foreign key from the super entity will be used through all sub entities would be helpful, either.

In the non-identifying relationship, the entity is in the reference relationship. Properties can be owned by a specific person, it still exists whether the person exist or not. Then what happens? The properties in the record would not be managed properly like the properties above. Nevertheless, mistaking a reference as a dependency would make a matter worse. (Imagine all properties being gone when a person dies.)

2. Identification dependency

The above kind of explanation will not be sufficient for its ambiguousness, as it seems to fix the relation between two entities. (Why a owner-property relation cannot be identifying?) Also, more fragile point from the existence dependency view is that every non-null FK means a child cannot exist without parent.

The identification dependency helps clear the ambiguousness. It is more meaningful in considering various situations.Imagine there are a team and a player. A player has a team, which is inserted as a FK `team-id`. If a player should not be identified without a team, `team-id` becomes the PK too. If a player can be identified without a team, `team-id` does not become PK. This explanation seems to be more flexible and to make sense.

The approach it has shows several advantages in my opinion: (1) Attributes migrated from the parent are handled through the design for identification, (2) An entity is clearly considered an independent entity. However, [The ERwin Data Modeler methods guide](https://ftpdocs.broadcom.com/cadocs/0/CA%20ERwin%20Data%20Modeler%20r8-ENU/Bookshelf_Files/PDF/ERwin_Methods.pdf) says that there is a risk that it might reflect the existence dependency.

3. Outro

The practice inside the business frequently uses the non-identifying relationship. The most important here would be the identifical correlation between the super entity and the sub entity, not only the practice itself. Although the points of view which the existence dependency and identification depedency was slightly different, researching both helped understad the notion of identifying realtionship. 

### References

https://documentation.softwareag.com/webmethods/compendiums/v10-7/C_Design_and_Implement_BPMs/index.html#page/design_implement_bpm_compendium/D76294.html

https://stackoverflow.com/questions/762937/whats-the-difference-between-identifying-and-non-identifying-relationships

https://ftpdocs.broadcom.com/cadocs/0/CA%20ERwin%20Data%20Modeler%20r8-ENU/Bookshelf_Files/PDF/ERwin_Methods.pdf