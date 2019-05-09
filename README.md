# App directory

1. Create root folder

```
mkdir .circleci
```

2. Create configuration yaml file

```
touch .circleci/config.yml
```

3. Add your configuration

```yml

# Version of circleci
version: 2
# What circleci have to do
jobs:
  # Do a build
  build1:
    # Version 2 of circleci uses docker
    # Circleci create an image of the environment where to run tests
    # using the custom dockerhub image circleci
    docker:
      - image: circleci/ruby:2.4.1
     # Steps to do
    steps:
      - checkout
      - run: echo "A first hello"
   build2:
    ...
  
workflows:
  version: 2
  wf1:
    jobs:
      - build1
      - build2
```

4. Push to repository


# Real world node example

```yml

version: 2
jobs:
  build:
    docker:
      - image: circleci/node:latest
    steps:
      - checkout
      - run: echo "npm install"
      - run: npm install
      - run: CI=true npm run build
  test:
    docker:
      - image: circleci/node:latest
    steps:
      - checkout
      - run: echo "tests"
      - run: npm install
      - run: npm test
workflows:
  version: 2
  build_test:
    jobs:
      - build
      - test
        
```
