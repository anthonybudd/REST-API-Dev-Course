# Migrations
Over the life-cycle of your app you will need to make changes to the database. To keep these changes uniform acrros the dev team and our hosting enviroments we save the history of the database design as code in our repo. These instructions to re-create the database are called migrations.

[Sequelize provides support for migrations](https://sequelize.org/master/manual/migrations.html).


### Naming Convention
It is very important to name your migrations correctly. All files in your `src/database/migrations/` folder must follow this naming convention.

```
YYYYMMDDHHMMSS-ACTION-TABLE.js

Exmaples:
20211224124959-create-Users.js
20220105100709-add-language-to-Users.js
20220126090304-remove-timezone-from-Users.js
```

By putting the date in that format the files will automatically sorted in chronalogical order. The name of the file after the Timestamp is less imprtant but descriptive naming will make long-term developmentr easier.

### Creating a Migration
Make a blank file in `src/database/migrations/` and name it appropriatly.

The `up` method will be executed when you are stepping 

The `down` method will be called in reverse.

20211224124959-create-Users.js
```js
module.exports = {
    up: (queryInterface, Sequelize) => queryInterface.createTable('Users', {
        id: {
            type: Sequelize.UUID,
            primaryKey: true,
            allowNull: false,
            unique: true
        },

        email: {
            type: Sequelize.STRING,
            allowNull: false,
            unique: true
        },

        password: Sequelize.STRING,
        name: Sequelize.STRING,           
    
        createdAt: {
            type: Sequelize.DATE,
            allowNull: true,
        },
        updatedAt: {
            type: Sequelize.DATE,
            allowNull: true,
        },
    }),
    down: (queryInterface, Sequelize) => queryInterface.dropTable('Users'),
};
```

Execuite the migrations using the command `npm run db:migrate`. This will create a table that looks like this.

| id | email | password | name | createdAt | updatedAt |
| ------ | - | - | - | - | - |
| &nbsp; |   |   |   |   |   |
| &nbsp; |   |   |   |   |   |

