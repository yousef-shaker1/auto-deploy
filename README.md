# auto-deploy

name: Deploy to Hostinger

on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy via SSH
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Deploy to Hostinger via SSH
      uses: appleboy/ssh-action@v1.0.0
      with:
        host: 45.87.81.237
        port: 65002
        username: u795677464
        key: ${{ secrets.HOSTINGER_SSH_KEY }}
        script: |
          cd /home/u795677464/domains/masr360travel.com/public_html/masr360
          git pull origin main
          php artisan config:clear
          php artisan cache:clear
          php artisan view:clear
          php artisan migrate --force
