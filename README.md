### Hi there 👋, I'm Neal Vo
#### Data Scientist (ML,AI)
![Data Scientist (ML,AI)](https://github.com/nealvo/nealvo/blob/main/tiny-cute-anime-robot-v0-56jsl91o7kba1.webp)

I'm Neal from Dallas, TX. and I'm currently Data Scientist at AT&T 

I really enjoy machine learning and AI. You can check out my Linkedln at https://www.linkedin.com/in/nealdvo/

Skills: Python / R / Power BI / Tableau / SQL

- 🔭 I’m currently working on this page. 
- 🌱 I’m currently learning AI & ML 
- 📫 How to reach me: https://www.linkedin.com/in/nealdvo/ 


[<img src='https://cdn.jsdelivr.net/npm/simple-icons@v4.0.0/icons/github.svg' alt='github' height='40'>](https://github.com/nealvo)  [<img src='https://cdn.jsdelivr.net/npm/simple-icons@v4.0.0/icons/linkedin.svg' alt='linkedin' height='40'>](https://www.linkedin.com/in/nealdvo/)  [<img src='https://cdn.jsdelivr.net/npm/simple-icons@v4.0.0/icons/twitter.svg' alt='twitter' height='40'>](https://twitter.com/DuyVo1330075)

# GitHub Action for generating a contribution graph with a snake eating your contributions.
name: Generate Snake

# Controls when the action will run.
on:
  schedule:
      # every 12 hours
    - cron: "0 */12 * * *"

  # This command allows us to run the Action automatically from the Actions tab.
  workflow_dispatch:
  
  # Also run on every push on the master branch
  push:
    branches:
    - main

# The sequence of runs in this workflow:
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      - name: Clone repo
        uses: actions/checkout@v3
    
      - name: Generate the snake files in './dist/'
        uses: Platane/snk@v3
        id: snake-gif
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
            dist/github-contribution-grid-snake.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
        env:
           GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Show build status
        run: git status

      - name: Push new files to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
          commit_message: Update snake animations
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
