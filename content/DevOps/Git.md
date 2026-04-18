## GitHub
 
 对于在Github私有repo或有访问权限的clone 可以先在github建一个personal token，然后使用
```sh
git clone https://username:<TOKEN>@github.com/username/reponame.git
```
进行clone

为了避免每次都push都要输入密码，可以先使用
```sh
git remote set-url origin https://username:<MYTOKEN>@github.com/username/reponame.git
```
配置好origin url, 之后每次push到 `origin branch`即可, 如`git push origin main`
