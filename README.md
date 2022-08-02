# Buy Online Backend

## Table of Contents

- [Description](#description)
- [Installation](#installation)
- [Technologies](#technologies-used)
- [Deployed Link](#link)
- [Usage](#usage)
- [User Information](#user-information)
- [Credits](#credits)
- [Questions](#questions)
- [License](#license)

## Description

This is the backend of an ecommerce site using Express.js and MYSQL. There are routes for products, categories, and tags: all of which can respond to GET, POST, PUT, & DELETE requests. See the provided link for a video walkthrough.

## Installation

Run this command to install this repositories dependencies:

```ruby
npm install
```

## Technologies Used

-Javascript
-Node.js
-Express.js
-MySQL
-Insomnia

## Usage

To initialize your database and start your server run the following commands:

```ruby
mysql -u root -p
source ./db/schema.sql
quit

npm run seed
npm run start
```

### Demo

![Walkthrough Demo of Backend Requests](https://drive.google.com/file/d/1QB4sVoQ9sg1rpOqU_itbaHuNJAwRJN7S/view)

### Code Snippets

Example of how the models where constructed. The one below is the model for products.

```ruby
Product.init(
  {
    id: {
      type: DataTypes.INTEGER,
      primaryKey: true,
      autoIncrement: true,
      allowNull: false,
    },
    product_name: {
      type: DataTypes.STRING,
      allowNull: false,
    },
    price: {
      type: DataTypes.DECIMAL,
      allowNull: false,
      isDecimal: true,
    },
    stock: {
      type: DataTypes.INTEGER,
      allowNull: false,
      defaultValue: 10,
      isNumeric: true,
    },
    category_id: {
      type: DataTypes.INTEGER,
      refereces: {
        model: "category",
        key: "id",
      },
    },
  },
  {
    sequelize,
    timestamps: false,
    freezeTableName: true,
    underscored: true,
    modelName: 'product',
  }
);
```

This is a get request for all products. All routes are configured to get all, get by id, post, put by id, and delete by id.

```ruby
router.get('/', async (req, res) => {
  try {
    const productData = await Product.findAll({
      include: [{ model: Category }, { model: Tag }],
    });
    res.status(200).json(productData);
  } catch (err) {
    res.status(500).json(err);
  }
});

```

## User Information

### **Michael Wence**

[LinkedIn](https://www.linkedin.com/in/michael-wence/) |
[GitHub](https://github.com/mtwence)

## Credits

UCB - Coding Bootcamp

## Questions

If you have any questions about this repository, you can contact me at mtwence@gmail.com.

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

© 2022 Michael Wence. All Rights Reserved.
