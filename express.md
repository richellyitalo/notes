# Arquivo estático
Para acessar `/files/{nome_arquivo}` da pasta `/tmp/uploads/{nome_arquivo}`

**https://expressjs.com/pt-br/starter/static-files.html**

Ex: 
```js
server.use(
  '/files/',
  express.static(path.resolve(__dirname, '..', 'tmp', 'uploads'))
)
```