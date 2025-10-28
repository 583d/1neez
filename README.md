name: Generate Snake

on:
  schedule:
    - cron: "0 0 * * *"   # runs daily at 00:00 UTC
  workflow_dispatch:       # allow manual runs

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Generate snake SVG
        uses: Platane/snk@v3
        with:
          github_user_name: YOUR_USERNAME
          outputs: |
            dist/github-snake.svg
      - name: Deploy to GitHub Pages (output branch)
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
