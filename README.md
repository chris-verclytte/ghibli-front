# ghibli-front · [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/chris-verclytte/ghibli-front/blob/master/LICENSE)
ghibli-front is a frontend consuming ghibli-back API is order to display list of Ghibli films including people involved in it.


## Project setup
```
yarn install
```

### Configure your API url
Add an `VUE_APP_API_URL` to the `.env` file at the root of the project.
For convenience a `.env` file is already committed to this repository and `VUE_APP_API_URL` defaults to `http://localhost:8001/api`.

### Compiles and hot-reloads for development
```
yarn serve --port 8000
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
