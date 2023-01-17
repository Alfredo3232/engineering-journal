# UDEMY NODE COURSE

1. ![Flex Container Features](images/image1.png "image_tooltip")
    <!--- MAIN SECTION SEPERATOR -->
2. ![Justify Content and Align Items](images/image2.png "image_tooltip")
    <!--- MAIN SECTION SEPERATOR -->
3. ![Align Content ](images/image3.png "image_tooltip")
    <!--- MAIN SECTION SEPERATOR -->
4. ![Flex Item Features](images/image4.png "image_tooltip")
    <!--- MAIN SECTION SEPERATOR -->
5. Font Awesome
    1. All of them are class and order of importance down.
        1. ```fas```
            1. `fas` is how font awesome is initialized or recognizes that this class is part of font awesome
        2. ```fa-<name-of-icon>```
            1. This is how you get an icon, you say fa- and then the name of the icon.
        3. ```fa-#x```
            1. This is how you get an icon to grow in size you say, fa- and then the number followed by an x, make sure to put this grow icon after the icon name.
    2. Change the icon color

        ```CSS
            # features i {
                color: color-here;
            }
        ```
    <!--- MAIN SECTION SEPERATOR -->
6. z-index
    1. z-index  css value this allows to put html content above others, z-index possible values are negative, zero and positive numbers
    2. z-index needs a position value or else it wont work as intended
        1. positions need to be fixed, absolute or relative
    <!--- MAIN SECTION SEPERATOR -->
7. Node
    1. _dirname
        1. What this is, is the location of your current directory.
    2. _filename
        1. What this is, is the location of your current directory plus the file name
    3. Module, exports & require
        1. module.exports is an object, so to export multiple things you can do this
            1. OLD -

                ```JS
                    module.exports.func = func
                ```

            2. NEW -

                ```JS
                    module.exports = {
                    func,
                    id
                    }
                ```

        2. Require

            ```JS
                const obj = require('<PATH>')
                obj.prop
            ```

    4. Event emitters
        1. How to read files
            1. ![alt_text](images/image5.png "image_tooltip")

        2. How to write and create files
            1. ![alt_text](images/image6.png "image_tooltip")

    5. ![alt_text](images/image7.png "image_tooltip")
        1. Number 1
            1. We are requiring a node package called http
        2. Number 3-6
            1. On number 3 that's how we create a server and it takes in a function
            2. On number 4 that's how we write the response we send a 200 and then what type of data are we sending
            3. On number 5 we are ending the response and sending a string called hello world
        3. Number 9
            1. We are listening to port 3000 and the other argument is saying what ip, that ip specifically that we are seeing is a localhost

    6. Server
        1. Buffer is a temporary storage for a data that's being transferred from one place to another
        2. ![alt_text](images/image8.png "image_tooltip")
        3. This is how you serve a html file, in a node server.
            1. ![alt_text](images/image9.png "image_tooltip")
        4. This is how you send a json response back
            1. ![alt_text](images/image10.png "image_tooltip")
        5. This is how you set up multiple endpoints
            1. ![alt_text](images/image11.png "image_tooltip")
        6. How to serve html files
            1. ![alt_text](images/image12.png "image_tooltip")
        7. Mongodb
            1. ![alt_text](images/image13.png "image_tooltip")
            2. ![alt_text](images/image14.png "image_tooltip")
            3.
