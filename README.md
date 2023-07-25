# Домашнє завдання 1

## Крок 1

- Ініціалізується npm в проекті
- В корені проекту створи файл `index.js`
- Постав пакет [nodemon](https://www.npmjs.com/package/nodemon) як залежність
  [nodemon](https://www.npmjs.com/package/nodemon) як залежність розробки
  (devDependencies)
- В файлі `package.json` додай "скрипти" для запуску `index.js`
  - Скрипт `start` який запускає `index.js` за допомогою `node`
  - Скрипт `dev` який запускає `index.js` за допомогою `nodemon`

## Крок 2

У корені проекту створи папку `db`. Для зберігання контактів завантаж і
використовуй файл [contacts.json](./contacts.json), поклавши його в папку `db`.

У корені проекту створи файл `contacts.js`.

- Зроби імпорт модулів `fs` (у версії, яка працює з промісами - `fs/promises`) і
  `path` для роботи з файловою системою
- Створи змінну `contactsPath` і запиши в неї шлях до файлі `contacts.json`. Для
  складання шляху використовуй методи модуля `path`.
- Додай функції для роботи з колекцією контактів. У функціях використовуй модуль
  `fs` та його методи `readFile()` і `writeFile()`
- Зроби експорт створених функцій через `module.exports`

```js
// contacts.js

/*
 * Розкоментуйте і запишить значення
 * const contactsPath = ;
 */

// TODO: задокументувати кожну функцію
function listContacts() {
  // ...твій код. Повертає масив контактів.
}

function getContactById(contactId) {
  // ...твій код. Повертає об'єкт контакту з таким id. Повертає null, якщо контакт з таким id не знайдений.
}

function removeContact(contactId) {
  // ...твій код. Повертає об'єкт видаленого контакту. Повертає null, якщо контакт з таким id не знайдений.
}

function addContact(name, email, phone) {
  // ...твій код. Повертає об'єкт доданого контакту. Повертає null, якщо контакт з таким id не знайдений.
}
```

## Крок 3

Зроби імпорт модуля `contacts.js` в файлі `index.js` та перевір працездатність
функцій для роботи з контактами.

## Крок 4

У файлі `index.js` імпортується пакет `yargs` для зручного парсу аргументів
командного рядка. Використовуй готову функцію `invokeAction()` яка отримує тип
виконуваної дії і необхідні аргументи. Функція викликає відповідний метод з
файлу `contacts.js` передаючи йому необхідні аргументи.

```js
// index.js
const argv = require('yargs').argv;

// TODO: рефакторить
function invokeAction({ action, id, name, email, phone }) {
  switch (action) {
    case 'list':
      // ...
      break;

    case 'get':
      // ... id
      break;

    case 'add':
      // ... name email phone
      break;

    case 'remove':
      // ... id
      break;

    default:
      console.warn('\x1B[31m Unknown action type!');
  }
}

invokeAction(argv);
```

Так само, ви можете використовувати модуль [commander]
(https://www.npmjs.com/package/commander) для парсинга аргументів командного
рядка. Це більш популярна альтернатива модуля `yargs`

```js
const { Command } = require('commander');
const program = new Command();
program
  .option('-a, --action <type>', 'choose action')
  .option('-i, --id <type>', 'user id')
  .option('-n, --name <type>', 'user name')
  .option('-e, --email <type>', 'user email')
  .option('-p, --phone <type>', 'user phone');

program.parse(process.argv);

const argv = program.opts();

// TODO: рефакторить
function invokeAction({ action, id, name, email, phone }) {
  switch (action) {
    case 'list':
      // ...
      break;

    case 'get':
      // ... id
      break;

    case 'add':
      // ... name email phone
      break;

    case 'remove':
      // ... id
      break;

    default:
      console.warn('\x1B[31m Unknown action type!');
  }
}

invokeAction(argv);
```

## Крок 5

Запусти команди в терміналі і зроби окремий скріншот результату виконання кожної
команди.

```shell
# Отримуємо і виводимо весь список контактів у вигляді таблиці (console.table)
node index.js --action="list"

# Отримуємо контакт по id і виводимо у консоль об'єкт контакта або null якщо контакту з таким id не існує
node index.js --action="get" --id 05olLMgyVQdWRwgKfg5J6

# Додаємо контакт та виводимо в консоль об'єкт новоствореного контакту
node index.js --action="add" --name Mango --email mango@gmail.com --phone 322-22-22

# Видаляємо контакт та виводимо в консоль об'єкт видаленого контакту або null якщо контакту з таким id не існує
node index.js --action="remove" --id qdggE76Jtbfd9eWJHrssH
```

## Крок 6 - Здача домашнього завдання.

Скріншоти виконання команд, можна залити на будь-який безкоштовний хмарний
сервіс зберігання картинок (Приклад: [monosnap](https://monosnap.com/),
[imgbb.com](https://imgbb.com/)) і відповідні посилання необхідно додати в файл
README.md. Створіть цей файл в корені проекту. Після прикріпіть посилання на
сховище з домашнім завданням в [schoology](https://app.schoology.com/login) для
перевірки ментором. Також у файл README.md треба додати посилання на репозиторій
зі зробленою роботою.

## Критерії прийому

- Створено репозиторій з домашнім завданням &mdash; CLI додаток
- Завдання відправлено менторові в [schoology](https://app.schoology.com/login)
  на перевірку (посилання на репозиторій)
- Код відповідає технічному завданню проекту
- При виконанні коду не виникає необроблених помилок
- Назва змінних, властивостей і методів починається з малої літери і записуються
  в нотації CamelCase. Використовуються англійські іменники
- Назва функції або методу містить дієслово
- У коді немає закоментованих ділянок коду
- Проект коректно працює з актуальною LTS-версією Node

<img src="https://lh3.googleusercontent.com/pw/AIL4fc-Nj1PFodmhaIZ2-6dylfKXpOjipApxxeCd89wlvwYuN3l8eL4z7kcm2noPuG1c7rUR22J-U9h1jqAUvPF7NJXDemCQZ_cm81QL_XMocaPVNaSGYzPOilZdAx2pyIIlHOB8ADG7MHPrH8n5uwDwEmAXE-7X5_vTAW67Z20OqD3qWuEILoCuSrqI6WECZG2SV9r0Bxn_BhebSLKZlK6dxEodp0QzPMd9JJSL6Yz34FVM1MHKD4Do0xI8vE9xCDZh182BrKNiK8aWOxWENUTPiKtDiTEB27UAjyrw0D1HKW-YsOMATpsi-GJwa9KbriRbdBUlWcnPLN60lr_A6NLtRS22iJNf0ckNZ9GlqGHLlA6i9Bp3avVbDmxoC3xUr9T6Btv-v71FdOQwnFFYcWM6W6xQmAUZsisj-J2Sl8SgbdOU0G8uMevP24bXXZXVvTPU0luyLj3px4GyH1n6TSh8dcU497Nwze21SB_R8iQ0lU94fx9EhIi1IeS_1qj_uH1dyrBaknsfUuwofknJ1DvAXjh-VYRhEhOKi5T39RxqsgFpXLnyB_ehs1US6YfvMu9tafgSYFFECqMG3Plz0iPd0mODyoukl8e-82XVSAO8_mp3YR13eZa92MQn8zjID9sR173O9HymXZ7zCw_TL2exQePqM01E_7DPVwSNyPyPCXrsH5VNGHkKIE3ttl5HuOA9-hf3fyidkPCqtW-A7bw5u9ZHuCGNhc23V4tfuedC4KBRQ_s4hn_I0KCHWHy0XxxC83VZvZA33ogc13gjiQOMfWtB0n9jA_DsNnmK2Hb5pywPyIhWKuYfoqmjOG6XhXX2F8h4UXvJx9vPlUtE701AG6QShOF-wGH-EyDIKbTlWea4irLwtvFkaypPNXMOTxHW0EMG8jB0Q6kxd3f2Ce67oONr27E=w717-h259-s-no?authuser=0">

<img src="https://lh3.googleusercontent.com/pw/AIL4fc-PzjgkxkKJS4Pd42G6iO7Mxsz97b0JM7598HSgFLG_gxnkGZ1FfunZ5ffyNeR8xQjHkQNPjnaW8vhbboQQZ6P5Y52wRFhuevVhdcRmdBTUoxGVWBVQN3ZCpgL-PAwZDsunkILVDd9NVCx8vEeK4Cf6WBavUWYr-jVenWxsgMwaYuxSCdxEe0ftZOHBCoBAo4T3DbvXtRxKMQo8bd04htQiycrpYbBVHGa-byXk2YegSm5xv1s9EWg3apCp2U44TQGr8YhPVLSgg44rbc6YHdpMyMWhehbHC9GtnZGUMuO76eQuJe60TPDXtqnPnRHlFuMiebxfDk8HSZlhMPhorejeKgwCOmbT7KNibkCYCH1K9-zY6d-bzW6GZv_LxUEPc5gPALEv7o9GjSAYdFWH_3Z1wOkPVTWZg__9xbfiiXgmfDMzpzgXVpwVNqEk2VNBJnlUVpv2fo6-6dvWqendN3i03tHioN3ho2UeI5_3XZq39cy3nLuRusz-mGAygSLqfYxvMcWzKeSHsTAb3ViFOw6-Io3C-SvEBUEz6ROYHL-VSiV77bLcnEdDulwbAHtIaNlkaUVrMDkkdCVrzmb48HmO72LlwyIfTkmjFzUx3QQmU5CW-Bo-2Xg0lH5VjbeIpKpYeiEy7s8CtNQJpZKZuNg-Geci84tu4Y313098MyVOA-ju7GOXzG_pDZbuXm24dc-rZedaa5h05mvWMN7qay9QOouzwBZcVGGmM-wFx90Xn_6JjWjGDbpr8zIsM1eHwCAs5tsBc3jsjZpYSBVgFx4MMqz8E3WqsG65HHo_3v6OAkJlXV2cBsUCASGmycBLW0B6SXFVnxLA6-p-sNqSiEHu7AVTGDK7GE4ZWi8ENoU1w6X2iLt9zjiOo-irSATKiZyOr7hnx0LFMtwtFr8HlZ-gLOc=w1119-h336-s-no?authuser=0">

<img src="https://lh3.googleusercontent.com/pw/AIL4fc-1gIiy1-6vSp0eC87Fu64OtEjoNj5iAv2pakkJRik8QxVt2Qs2cHl8KwolXk5U4KsNPfApEB59z50YeRdrg8dF68IppzaHmrFwVd55FtSsFD66fRH_Q6SsjaHez5rd-z-q-p9ufDMVlHctYz7bKTKN2oQzV4k0xMiKdnI3qukADdM4APoXhCh0CMIjZFdSHeunCSzu3_ppT3N9VPBS5tGStO4qNSki_OSZwa4dtWvn-inWmvH_XAYwL1hbCSlP5gMWGqqaPqZ2tUb9qMiI-D7ZqhvaJlnHOlovSVgsEJwrQ5DYoSEGZhu7eYy7KWn2lyf7bVgR6LRpTW1xbDYTtA0wgf5wuwa-wFfyQ00o1vM-uFOUDvT5nLKnT4DJVgZkTZFPcqroCz9fH70LBbuBa3LfI_tVg_JMYV6tCtYDUWAkPFysuVu0KcGRHqfhq-262fqRAjf-SdiYNCHOIGuyheaTrhFMhI_YexbjGYd79dgJKECVDrChRcy-d8flBohB02fE11OvmBGH-57pDcP68xgkpWdTirZRkUYYZiLK3yOkgTaBnbYeHBnp07vQiEmumWPgHNcZ0k0CfKsNPb3zCCar7nWFK8e6Lo-p0rxw6XEQ4Yi1BmtndSGA3XOqLunGoduNaMvGuBklHIwPSi_02f8OokEJwX6vAnYHXzfTJc04R0Uzi9k90b1HLMEI1qvHTrXdxnQTOdirRm8sCWcXHUsBCVSUc6_yb8E84pifqoxMK0hWstmhypw-NgzjGpu2ffNT6YQUvzl8edFCNT3wLAb86lqKtpaf3jvOR2qOmPH45LL94e4Bs0KtsCJ9P4f_e1uJ0AHSDkJyy-iFBFc3-Qmx7wkoUZ_CRYcQG9lcF7w15YQoGtNIXkF8vd-r4uEXOd1RQcqQLoFtaBcyNqAqdyf3LoI=w748-h352-s-no?authuser=0">

<img src="https://lh3.googleusercontent.com/pw/AIL4fc_hQ6ltqVgmB98bZmX73QNRcvZ31GUNEaQuJeDDPDpl9uxdK-RIJcWhxbnGyrFJd7F_kkITPXRIf6MBLNQKWWvTgX7PC65vcA1BR-kCkLj6RP4sur8MkXqgD_0PlrIHlsyIvfy7lM7T9uo7qIOliwX0Hss8bNW1c6_mrQd8lwetVYY2teDnsrnftCB1plaquxRFPkM8ycIYywRCVOTRTNx0zH5hVVvUDRR_H7SKVT2dWy903zxe3sZE7XBN1hZmzeeZEOx6HIwD2froOFHItMeRvo2NXtyk58E9IvBoq-8RFZIEpSi-_HCfp1LLFSP8eWLdwLyaQyh68ZoSIR41BUG_jfBR2dOmj4o1Ry7bEzS_uLvPML_Jqq9hBJMCIWg_MlXg7haoztnKh5-GvNmOuSCUV1OsbuVI4MUu8T7PTxrXtBo77wlL8ll64DDXevD97V-0ck4PIxjpQIeX5Lmy9BMsZk9aPPlUASnAQcQYwU7xB3l5YpmfYYr0sCV2o8Ryv8Yx_qULZuEhKAX5tLs9tBEMk563TEOuS8mkbE-A9XU7dnK9t8kXEcOiutkrzc1ojAWFXrtV-l7TtMtgOKDanHSquqEctAr_p5vjX_NU-VFD21pYwJEj8DHyjo0a0JtxJNHpls7PZYpyrcWRflqzMnBw_8XG2JxMkWxFpk9jPifWR-WsQQOgAXXjZK7BPpY9d1Qp2VDHc5E6Io6pXIKPBLc6mM4vUqyfG6NWPpOUau-d_Ax8uIRmC-lZhuHuljjxrB9f8TP1jsRU8cB8WoRDwlzsHs2oJw9E6eI7PkgQ0RoFdS5Tc33SFvL8LpijsjgolPH56GVNRAJ24AaTEFXktvig4yfUG8KJQjk3RQCpp_A1ZQwtss_gNCmkuE7SU4M0xp-Rn_8ReoRUhk9t_5yiEyWlGOM=w1184-h469-s-no?authuser=0">

<img src="https://lh3.googleusercontent.com/pw/AIL4fc-fpNbjGizov4twvDRFpJGC7j_EY8aF5SnISWlCIhOPhwi_YHRywpTGmGYhXCiIt-g7ZQ0loB5n55Fk73zkhNq6ypB2yyt6Q0bfmqsrh3z3h1dwdr4yDS4oLYff9VXes2nYzCsjrFHruNqQoQeX3MyW4xqC5PO0G4ExG4LHe3C_QtntHyjofReZXtvkLvX61ROLiGh9xZu50bq_h-XWvyic54MZB4Ztm8a7Cm2VC26TRvBbHBmgAQdzHY8SNT-RtsNdIpJESUG_OUEAmDkenfwGI2A0R94tygwi6eGaK7Jj3n8kbRc4e14X-EkelUTpqUEXxXZnIxZmVFWEkDu896VuJDWl59as26cWfGKSgivpI6mouE77P6cJmKagm1Vq5Fqbh0F1DK6I3yJ8FGhf66vbSgWb_-hXPXnzKJFl6OtgPlaHjASawygrIRz4mXOBYMpDNq9pPaX9-hhNgjl8mnaWV8OXXt38el5x7a8R7cQIL9dVDSIt1rcI3xUoFXh_IGh5IswX7GDbyYcxLDb4hri3JGL1RKL7elPZi0PvvtAeO6NAQSnZxdmTQBiZhDewIa-8TZLk1R_Uy3XE9NhY04hBwa8UYCj64KpscbNBx2fpRjN4cV4mD6Osp6Z64u0mjtHNXz7pnZy5peV0QpKC3jkr_dSPCqvMNnQHY7QfdhabGo2sn8JLFFcqfrwqYh98diL1TiynYWiqlHAlDBl7qddNFwzsze50AhfgjTCK78W6HAmPVvEmCrHMmc201LOaG7CvOJXaRzperK26jAR3dVvLkbMH8gPho-jwPxWFG_qT5GRhmJrQX0xgSiu4qcX_nEAQtzmvq61tcbh9uuFYU5Z8n4tbnkaqaAufpS457wYX-GWQfBTHmc-lvZ758MX3VsXMzug0Pdw2MhoDVVRDJrNWF4I=w824-h345-s-no?authuser=0">
