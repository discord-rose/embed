# JaDL Embed

Simple and easy to use embed renderer

```js
const embed = new Embed()
  .title('Hello world!')
```

In order to get the raw API embed you do `embed.render()`

## Custom sendback

Which this embed, you can create sendbacks that allow you to use nested .send() methods

For example

```js
const embed = new Embed((embed) => {
  // embed being the created embed object

  console.log(embed.render())
})

embed
  .title('Hello!')
  .send() // this will run back the sendback passed in the constructor
  // => logs { title: 'Hello!' }
```

This is super useful for creating nested library functions e.g, how we do it in JADL is a .embed method that returns a new embed, and handles the .send() seamlessly to it's context

### In TS

You can also create custom return types and paramater names like so:

```ts
const embed = new Embed<
  Promise<APIMessage>, // sets the return type of .send
  [ // options
    reply?: boolean,
    mention?: boolean
    // etc
  ]
>((embed, options) => {
  // options will now be typed as [boolean?, boolean?]

  return API.sendMessage(embed.render()) // return your Promise<APIMessage>
})

embed
  .title('Hello!')
  .send(true, true) // this will be typed as your options
  // the return type of this is Promise<APIMessage>
```