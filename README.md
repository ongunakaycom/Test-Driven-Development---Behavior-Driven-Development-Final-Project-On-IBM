# TDD / BDD Final Project Template

This repository contains the template to be used for the Final Project for the Coursera course **Introduction to TDD/BDD**.

## Usage

This repository is to be used as a template to create your own repository in your own GitHub account. No need to Fork it as it has been set up as a Template. This will avoid confusion when making Pull Requests in the future.

From the GitHub **Code** page, press the green **Use this template** button to create your own repository from this template. 

Name your repo: `tdd-bdd-final-project`.

## Setup

After entering the lab environment you will need to run the `setup.sh` script in the `./bin` folder to install the prerequisite software.

```bash
bash bin/setup.sh
```

Then you must exit the shell and start a new one for the Python virtual environment to be activated.

```bash
exit
```

## Tasks

In this project you will use good Test Driven Development (TDD) and Behavior Driven Development (BDD) techniques to write TDD test cases, BDD scenarios, and code, updating the following files:

```
tests/test_models.py
tests/test_routes.py
service/routes.py
features/products.feature
features/steps/load_steps.py
```

You will be given partial implementations in each of these files to get you started. Use those implementations as examples of the code you should write.

## Author

John Rofrano, Senior Technical Staff Member, DevOps Champion, @ IBM Research

## © IBM Corporation 2023. All rights reserved.

---

## Exercise 1: Create Fake Products

In the `tests/factories.py` file, use the Faker providers and Fuzzy attributes to create fake data for the `name`, `description`, `price`, `available`, and `category` fields by adding them to the `ProductFactory` class.

### Solution

```python
class ProductFactory(factory.Factory):
    """Creates fake products for testing"""

    class Meta:
        """Maps factory to data model"""

        model = Product

    id = factory.Sequence(lambda n: n)
    name = FuzzyChoice(
        choices=[
            "Hat", "Pants", "Shirt", "Apple", "Banana", "Pots", "Towels", "Ford", "Chevy", "Hammer", "Wrench"
        ]
    )
    description = factory.Faker("text")
    price = FuzzyDecimal(0.5, 2000.0, 2)
    available = FuzzyChoice(choices=[True, False])
    category = FuzzyChoice(
        choices=[
            Category.UNKNOWN,
            Category.CLOTHS,
            Category.FOOD,
            Category.HOUSEWARES,
            Category.AUTOMOTIVE,
            Category.TOOLS,
        ]
    )
```

---

## Exercise 2: Create Test Cases for the Model

Before we proceed with creating test cases for the Product Model, here are the different attributes used in this model:

| Attribute   | Description                                       |
| ----------- | ------------------------------------------------- |
| id          | The ID of the product                             |
| name        | The name of the product                           |
| description | The description of the product                    |
| price       | The price of the product                          |
| available   | True if the product is available, otherwise False |
| category    | The category under which the product belongs      |

Please refer to the course reading *"About the Product Model"* to understand the classes and methods used in the `models.py` file.

### Task

Create test cases in `tests/test_models.py` to exercise the code in `service/models.py` to test that the Product model works.

1. Write test case to read a product and ensure that it passes
2. Write test case to update a product and ensure that it passes
3. Write test case to delete a product and ensure that it passes
4. Write test case to list all products
5. Write test case to search for a product by name and ensure that it passes
6. Write test case to search for a product by category and ensure that it passes
7. Write test case to search for a product by availability and ensure that it passes

---

## Exercise 3: Create Test Cases and Code for REST API

Now that you know that the model is working, you can move on to developing the REST API which will accept JSON requests, call the model, and return an answer as JSON.

Your REST API must implement the following endpoints:

* Create a Product
* Read a Product
* Update a Product
* Delete a Product
* List all Products
* List Products by Category, Availability, and Name

### Task

Edit the test cases in `tests/test_routes.py` and code in `service/routes.py` for a RESTful endpoint using Flask that contains the following endpoints:

1. Write a test case to Read a Product and watch it fail
2. Write the code to make the Read test case pass
3. Write a test case to Update a Product and watch it fail
4. Write the code to make the Update test case pass
5. Write a test case to Delete a Product and watch it fail
6. Write the code to make the Delete test case pass
7. Write a test case to List all Products and watch it fail
8. Write the code to make the List all test case pass
9. Write a test case to List by name a Product and watch it fail
10. Write the code to make the List by name test case pass
11. Write a test case to List by category a Product and watch it fail
12. Write the code to make the List by category test case pass
13. Write a test case to List by availability a Product and watch it fail
14. Write the code to make the List by availability test case pass

---

## Exercise 4: Load BDD Background Data

The first thing you will need to do for BDD testing is write the Python code to load the data from the `Background:` statement in the `products.feature` file.

The data is stored in the `context.table` attribute and each row is a Python `dict` that you can dereference using the names at the top of the columns in the `Background:` statement.

### Task

Update the `features/steps/load_steps.py` file to load background data from your BDD scenarios into your service before each scenario executes.

The code to delete all of the products is already given to you. You just need to write the code to load the products from `context.table`.

---

## Exercise 5: Create BDD Scenarios

Now that the background data is loaded, it's time to write the scenarios to test the UI.

The `Create a Product` scenario is already written as an example of what you need to do.

The service already contains a UI that looks like this:

![UI Screenshot](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/final-product-ui.png)

### Task

Update the `features/products.feature` file with BDD Scenarios that prove that the following behaviors of the UI work as expected:

1. Read a Product
2. Update a Product
3. Delete a Product
4. List all Products
5. Search for Products by Category
6. Search for Products by Availability
7. Search for Products by Name

---

## Exercise 6: Implementing Steps

In BDD, test scenarios are written in a human-readable format (e.g. Gherkin) and these are translated into automated tests using step definitions.

The `web_steps.py` file contains the step definitions for the web-related actions on the UI.

Please check the course lab titled *"Implementing Your First Steps"* for reference before proceeding.

### Task

Update the `features/steps/web_steps.py` file with the remaining step definitions.

Start by opening the file `web_steps.py`.

## 🤝 Contributing

Pull requests and feedback are welcome! If you'd like to contribute improvements, feel free to fork and submit a PR.

---

## About Me

I'm Ongun Akay, a Senior Full-Stack Developer with expertise across various technologies.

- 👀 I specialize in full-stack development with extensive experience in frontend and backend technologies.
- 🌱 Currently, I'm sharpening my skills in advanced concepts of web development.
- 💞️ I’m always open to exciting collaborations and projects that challenge my abilities.
- 📫 You can reach me at [info@ongunakay.com](mailto:info@ongunakay.com).

---

## 📄 License

This project is licensed under the [Apache-2.0 license](./LICENSE) — see the LICENSE file for details.
