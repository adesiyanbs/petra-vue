# Petra Inline Checkout for Vue

## NPM Installation

Run the command below in your Terminal to Install the component

```bash
npm i petra-vue
```

### Importing the petra-vue

Go to your component and import the Component and add it in your component as suggested below

```js
import PetraVue from "petra-vue"

export default {
  name: 'App',
  components: {
      PetraVue
  },
}
```

### Feeding the component with the write data

You are to feed the component with the checkout data using the data object, and the function you want to run when the checkout is canceled on **onClose** and the function to run when the checkout is completed on **onSuccess**

```html
<petra-vue
   :data="data"
   :onClose="onClose"
   :onSuccess="onSuccess"
 />

```

In **clientInfo** here you have various variables that is needed to complete checkout

- Amount: Amount to be processed
- Email: Email of your customer
- Key: Api Key automatically generated for you on Petra 
- Button: The CSS styling of your button

## Example Payload 

```javascript

  data() {
    return {
        data:{
            amount: 100000,
            email: 'test@gmail.com',
            key:'pk_test_U4GzNZdtkqC0Oxkdi4FkmH9JLNcE1DKe',
            button : {
                backgroundColor: "#E1b234",
                border: "none",
                borderRadius: "10px",
                color: "white",
                textAlign: "center",
                textDecoration: "none",
                height: "50px",
                width: "250px",
                display: "inline-flex",
                alignItems: 'center',
                justifyContent: 'center',
                fontSize: "14px",
                transitionDuration: "0.4s",
                cursor: "pointer",
                padding: "10px 32px",
                opacity: "1"
            }
        }
    }
 },
```
You can add the method for closed checkout on ``onClose()`` and for completed checkout ``onSuccess()``

```js
  methods: {
    onClose(){
      alert('It Closed oo')
    },

    onSuccess: ()=>{
      alert('It Succeeded oo')
    }
  }
```
