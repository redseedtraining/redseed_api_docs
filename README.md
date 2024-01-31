To run the build process locally for testing and debugging purposes, follow these steps:

1. Make sure you have Docker installed on your machine.

2. Open a terminal and navigate to the root directory of the project.

3. Run the following command to serve the documentation locally:
```
docker run --rm --name slate -p 4567:4567 -v $(pwd)/source:/srv/slate/source -v $(pwd)/data:/srv/slate/data slatedocs/slate serve
```

4. Open your web browser and visit http://localhost:4567 to view the documentation.

5. To build the documentation locally, run the following command:
```
docker run --rm --name slate -v $(pwd)/build:/srv/slate/build -v $(pwd)/source:/srv/slate/source -v $(pwd)/data:/srv/slate/data slatedocs/slate build
```

After running the build command, the generated documentation will be available in the "build" directory.

Please note that these commands assume you are running them from the root directory of the project and have the necessary Docker setup.

To replicate the GitHub Actions build process, you can use the same commands mentioned above. The GitHub Actions workflow already sets up the required environment and executes these commands to build the documentation.
