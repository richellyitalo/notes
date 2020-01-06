# Arquivo estático

Para acessar `/files/{nome_arquivo}` da pasta `/tmp/uploads/{nome_arquivo}`

**https://expressjs.com/pt-br/starter/static-files.html**

Exemplo

```js
server.use(
  '/files/',
  express.static(path.resolve(__dirname, '..', 'tmp', 'uploads'))
);
```

# Retorno de dados relacionados (com Sequelize)

**https://sequelize.org/master/manual/querying.html#attributes**

Exemplo
```js
const providers = await User.findAll({
  where: { provider: true },
  attributes: ['id', 'name', 'email', 'avatar_id'],
  include: [
    {
      model: File,
      as: 'avatar',
      attributes: ['url', 'name', 'path']
    }
  ]
});
```
