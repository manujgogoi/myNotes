`<projectRoot>/.github/workflows/node.js.yml`

```yml
name: Node.js CI

on:
  push:
    branches: ["main"]

jobs:
  build:
    runs-on: self-hosted

    strategy:
      matrix:
        node-version: [20.x]
    env:
      PORTFOLIO_URL: ${{secrets.PORTFOLIO_URL}}

    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
          cache: "npm"
      - run: npm ci
      - run: npm run build --if-present

      # Navigate to the application directory
      - name: Navigate to Application Directory
        run: cd /home/manuj/actions-runner/_work/portfolio/portfolio/

      # Stop existing PM2 process
      - name: Stop PM2 Process
        run: pm2 stop dl_portfolio || true

      # Start PM2 Process
      - name: Start PM2 Process
        run: pm2 start dl_portfolio
```
