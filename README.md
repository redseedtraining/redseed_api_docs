docker run --rm --name slate -p 4567:4567 -v $(pwd)/source:/srv/slate/source -v $(pwd)/data:/srv/slate/data slatedocs/slate serve


docker run --rm --name slate -v $(pwd)/build:/srv/slate/build -v $(pwd)/source:/srv/slate/source -v $(pwd)/data:/srv/slate/data slatedocs/slate build
