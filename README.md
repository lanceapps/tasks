name: Release Charts

on:
push:
branches:
- main

jobs:
release:
runs-on: ubuntu-latest
steps:
- name: Checkout code
uses: actions/checkout@v2

      - name: Setup Helm
        uses: azure/setup-helm@v1

      - name: Run chart-releaser
        env:
          CR_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          helm repo index ./charts --url https://<your-github-username>.github.io/<your-repo-name>
          npx chart-releaser upload --owner <your-github-username> --repo <your-repo-name> --token ${{ secrets.GITHUB_TOKEN }}
