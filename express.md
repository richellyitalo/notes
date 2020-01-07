## Static files

To access `/files/{nome_arquivo}` from folder `/tmp/uploads/{nome_arquivo}`

**https://expressjs.com/pt-br/starter/static-files.html**

Example
```js
server.use(
  '/files/',
  express.static(path.resolve(__dirname, '..', 'tmp', 'uploads'))
);
```

## Returning related data (with Sequelize)

**https://sequelize.org/master/manual/querying.html#attributes**

Example
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

## Configuring Nodemailer with handlebars
```js
import nodemailer from 'nodemailer';
import expresshbs from 'express-handlebars';
import nodemailerhbs from 'nodemailer-express-handlebars';
import { resolve } from 'path';
import mailConfig from '../config/mail';

class Mail {
  constructor() {
    const { host, port, secure, auth } = mailConfig;

    this.transporter = nodemailer.createTransport({
      host,
      port,
      secure,
      auth: auth.user ? auth : null,
    });
    this.configureTransporter();
  }

  configureTransporter() {
    const viewPath = resolve(__dirname, '..', 'views', 'emails');

    this.transporter.use(
      'compile',
      nodemailerhbs({
        viewEngine: expresshbs.create({
          layoutsDir: resolve(viewPath, 'layouts'),
          partialsDir: resolve(viewPath, 'partials'),
          defaultLayout: 'default',
          extname: '.hbs',
        }),
        viewPath,
        extName: '.hbs',
      })
    );
  }
}

export default new Mail();
```
