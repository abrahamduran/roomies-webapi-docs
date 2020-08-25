# Getting Started

This is where it all begins...

The Roomies RESTful API is here! The idea behind this API is to help us manage our financial
headaches in a more automated way. This WebAPI will:

- Manage **expenses**
- Manage **payments**
- Aid in the **distribution** of expenses
- Let you quickly see your **balance**
- Keep **track** of the expenses and payments, where's the money going?

Some ideas for the future are:

- Support login/signup
- Notify members when an expense in registered for them
- Notify members when a payment has been made to them

The API resides at <https://api.roomies.do>, and there is a beta version you can find at <https://dev.roomies.do>.
Keep in mind you will need to be connected to the local network for this to work, as this domain names are resolved locally.
::: warning HTTPS Certificate
The APIs are served behind a reverse proxy that will enforce all request are made using HTTPS.
However, because this domains are registered locally, there's no way for a CA authority to emit
a certificate (because it cannot verify the identity of the server). For this, a local certificate
was emitted. Your browser will not trust that certificate by default (it's local after all), therefore
it will complain about it.
:::

::: tip
Head over to <https://demeter.do/cert/>, download and install the `rooCA.pem` to silence your browser's complains.
:::
