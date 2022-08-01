## Levantar el proyecto 

1. Instalar rvm. Ref:  [Instalar RVM](https://nrogap.medium.com/install-rvm-in-macos-step-by-step-d3b3c236953b)
2. Setear version de ruby 3.1.2 con 
   ```javascript
$ rvm install 3.1.2
$ rvm alias create default 3.1.2
    ```
2. Instalar just-the-docs con: ``gem install just-the-docs``
3. Instalar eventmachine con: ``gem install eventmachine -- --with-cppflags=-I/usr/local/opt/openssl/include``
4. Instalar depedencias con: ``bundle install``
5. Levantar el proyecton con: ``bundle exec jekyll serve``
6. Se levanta localmente en [localhost:4000](http://127.0.0.1:4000)
