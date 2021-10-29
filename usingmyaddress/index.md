# Using My Address With Github Pages

# 如何將gihub pages導向到自己申請的網址
## 第一步 架一個自己的網站
- 如何架一個部落格，請看[小十的部落格](https://blog.smallten.tk/p/hugo-01/)
## 第二步 申請 domain name 並增加一個 cname
- 想申請免費的 domain name ? [freenom](https://www.freenom.com)
  - 不過freenom申請的免費域名期限最多是一年喔
  - 快到期時會寄 email 通知，到時候就可以再續一年啦~
- 設置cname
   1. 點選 freenom 的 service 下的 My Domains  
   ![](/images/cname.jpg)
   2. 點選 `Manage Domain`  
   ![](/images/cname(1).jpg)
   3. 點選 `Manage Freenom DNS`  
   ![](/images/cname(2).jpg)
   4. 輸入自己要的 cnmae 並選好 type
   5. Target 則輸入 `[YOUR].github.io`  
   ![](/images/cname(3).jpg)
## 第三步 更改github 上的 workflows
- 在deploy 後面加上 `cname: [YUOR CNAME]`， ex:`cname: 'blog.mantoto.tk'`
```
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          cname: [YUOR CNAME]
```
---完成囉---

