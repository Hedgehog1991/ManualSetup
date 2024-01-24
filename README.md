# ManualSetup
testing minimal setup with vite, react, pages.

create a repo with a readme file.
New - Project from version control:
Your github repo code url.

In local project create index.html
fill it with basic content.
Add h1 tag and write something in it.

In lo project cmd run.
npm install --save-development vite
npm pkg set scripts.dev=vite
npm install react react-dom
npm install typescript
 npm install ol

create a .gitignore and add
````
.idea/
node_modules/
/dist/

````
Make sure package.json looks like this.
````
{
  "dependencies": {
    "ol": "^8.2.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "typescript": "^5.3.3",
    "vite": "^5.0.12"
  },
  "scripts": {
    "dev": "vite",
    "build": "vite build"
  }
}
````
In cmd:
npm run build.

Go to github Repo/settings/pages
Build and deployment Source = Github Actions
Go to github Repo/settings/Actions
Workflow permissions = Read and write permissions

Create a folder in the local project:
.github/workflows
make a file in it called:
node.js.yml

Fill it with the below code.
Make sure it looks like this.

````
# This workflow will do a clean installation of node dependencies, cache/restore them, build the source code and run tests across different versions of node
# For 2 more2 information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

name: Node.js CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [18.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'
      - run: npm ci
      - run: npm run build --if-present
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: './dist'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

````

Push to github = finished.