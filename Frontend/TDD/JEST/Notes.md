# TDD with JEST

1. In our project we first started by creating and starting our folder and environment.
    1. We created a folder called Todo-TDD
    2. We did npm init -y, to initialize our package.json
    3. So far we have installed the following packages
        1. Express for the server
        2. Mongoose for our database
        3. Node-mocks-http to imitate requests and responses used in our tests
2. We then started our server using express
3. Now onto testing, we created a folder called tests and another folder called unit. After that we created a file called todo.controller.test.js. Then on the origin of our project we created another folder called controllers and a file called todo.controller.js
    4. From what I got from this so far and reading documentation is that:
        4. JEST reads files that are named like this format
            1. name.test.js
        5. `.test` seems like JEST reads those files
4. After that we decided to begin, on our test file we required todo.controller.js, then we wrote this

```JS
describe("TodoController.createTodo", () => {
    it("should have a createTodo function", () => {
        expect(
           typeof TodoController.createTodo
        )
        .toBe("function");
    })
};
```

5. In order to run our test we had to change in our package.json, change the stuff that was in test in scripts to just jest
6. By running this it made jest automatically run without telling it where to look, it ran the test and failed like expected

# JEST ARCHITECTURE

1. Jest is split up into multiple packages
    1. jest-cli - is a legacy package used for people who installed jest-cli wouldn’t have to migrate to jest
        1. this is mainly used now to call other packages in a order
    2. jest-config - figure out what should have happen based specified on a config based on jest config file package.json
    3. jest-haste-map - this checks for all the files in the project and what are their dependencies between the files
        1. The way it does this it looks for require calls or import calls and goes down the tree. It's more like a map and goes down and extracts them and loads them.
        2. This also calls watchman - (it only calls this if you have it installed) this is used to keep track of all the changes in your files, then caches them to jest-haste-map. So that next time when jest is run it gives it the list of changed files, added files, removed files, …etc.
        3. This also calls jest-worker - this is a module used to see how many cores does your PC have and ideally uses most of them to process the above faster
