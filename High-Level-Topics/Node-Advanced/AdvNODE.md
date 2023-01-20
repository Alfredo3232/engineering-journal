# Advanced NodeJS

1. Internals with NodeJS
    1. Two most important components of NodeJS that is being used is
        1. V8 Project
            1. It's an open source javascript engine created by google, its purpose is to be able to execute javascript code outside the browser.
        2. libuv project
            1. It's a C++ open source project that gives node access to the operating system’s underlying file system and networking.
    2. Why do we use NodeJS then
        1. Javascript developers write javascript, not c++ which most of these projects above are written in c++
        2. NodeJS is bundled with multiple library modules such as
            1. http
            2. fs
            3. crypto
            4. path
        3. ![alt_text](images/image1.png "image_tooltip")
    3. NodeJS Event Loop
        1. ![alt_text](images/image2.png "image_tooltip")
        2. ![alt_text](images/image3.png "image_tooltip")
        3. NodeJS is not truly single threaded, there are other threads that node uses for doing some computationally intensive tasks ![alt_text](images/image4.png "image_tooltip")
        4.
