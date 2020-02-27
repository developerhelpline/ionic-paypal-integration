# Ionic 4 PayPal Payment Integration — for Apps
Ionic 4 with Paypal integration. App

### Table of Contents
- What is Paypal?
- What is Ionic 4?
- Ionic 4 and Payment Gateways

### What is Paypal?

PayPal is one of the most popular and easiest payment gateways to integrate into your website or application. It is also distributed throughout the world, promoting a wide range of payment options. Together with Stripe, PayPal can handle almost all of your payment requirements so you don't have to go anywhere.

### What is Ionic 4?

Ionic System is an open source UI toolbox for building performant, top notch versatile and work area applications using web progresses (HTML, CSS, and JavaScript). Ionic System is fixated on the frontend customer inclusion, or UI cooperation of an application (controls, keen, movements, activitys). It's easy to retain, and organizing enjoyably with different libraries or frameworks, for example, Precise, or can be used independent without a frontend framework utilizing a fundamental content fuse.

So, in other words — If you make Local apps in Android, you code in Java. On the off chance that you make Local apps in iOS, you code in Obj-C or Quick. Both of these are capable but complex dialects. With Cordova (and Ionic) you'll compose a single piece of code for your app that can run on both iOS and Android (and windows!), that as well with the straightforwardness of HTML, CSS, and JS.

### Ionic 4 and Payment Gateways

Ionic 4 can make a wide assortment of apps, and subsequently a wide assortment of installment portals can be actualized in Ionic 4 apps. The well known ones are PayPal, Stripe, Braintree, in-app buy etc.

PayPal can be coordinates in websites as well as portable apps. There are diverse ways of integration of PayPal SDK. In this web journal we’ll learn how to coordinated PayPal installment portal in Ionic 4 apps and Ionic 4 PWA.

[![Ionic 4 PayPal payment integration — for Apps and PWA](https://www.developerhelpline.com/wp-includes/images/ionic-paypal.jpeg "Ionic 4 PayPal payment integration — for Apps and PWA")](https://www.developerhelpline.com/wp-includes/images/ionic-paypal.jpeg "Ionic 4 PayPal payment integration — for Apps and PWA")

We are going learn how to actualize Paypal installments for an Ionic 4 versatile app. We are able break down the post in these steps:

**Step 1** —  Creating an Ionic 4 app. We are going utilize the Ionic 4 clear starter.

**Step 2**  —  Make a PayPal designer account and arrange it for app and PWA integration.

**Step 3**  —  Utilize Ionic Native plugin for PayPal to empower installment in versatile apps.

**Step 4**  —  Build the app on android to test app payments.

**Step 5**  —  Configure PayPal web integration with Javascript.

**Step 6**  —  Run the PWA on `ionic serve` to test web payments.

## Step 1  —  Create a basic Ionic 4 app

Making a fundamental Ionic 4 app is much simple. Expecting you've got all fundamental necessities introduced in your framework, run

```javascript
$ ionic start ionic-paypal-integration blank
```

This creates your app with title `ionic-paypal-integration` and blank template.

With minor alterations, my homepage looks like this.

[![Paypal payment homepage](https://www.developerhelpline.com/wp-includes/images/paypal-payment-homepage.jpg "Paypal payment homepage")](https://www.developerhelpline.com/wp-includes/images/paypal-payment-homepage.jpg "Paypal payment homepage")

## Step 2 — Configure a PayPal developer account

To arrange PayPal payments in your Ionic 4 app, you need to make a business PayPal account. For testing purposes, you'll utilize the Sandbox test accounts. Sandbox testing will see precisely like live installments, but it won't deduct any cash from your account or Credit Card.

To obtain your Sandbox credentials follow the steps below:

1. Go to [Sandbox Accounts](https://developer.paypal.com/developer/accounts/ "Sandbox Accounts") and create a sandbox business and personal test accounts.

2. Go to [My Apps & Credentials](https://developer.paypal.com/developer/applications/ "My Apps & Credentials") and generate a [v.zero](https://developer.paypal.com/docs/bt-vzero-overview/ "v.zero") SDK sandbox credential and link it to your sandbox test account. You need a Sandbox account to make payments in Sandbox mode of your app. In other words, when your app's PayPal SDK is running in Sandbox mode, you cannot make payments with an "actual" PayPal account, you need a Sandbox account.

3. Go to [My Apps & Credentials](https://developer.paypal.com/developer/applications/ "My Apps & Credentials")s and create an app. This is the app associated with your payments. A PayPal account can associate multiple such apps with it (you can redirect money from multiple mobile or web-apps in a single PayPal account).

[![Create new app in PayPal account](https://www.developerhelpline.com/wp-includes/images/paypal-my-accounts.jpg "Create new app in PayPal account")](https://www.developerhelpline.com/wp-includes/images/paypal-my-accounts.jpg "Create new app in PayPal account")

Also note down your Client ID from the app details. This is mostly what you need to integrate PayPal in your app and test payments.

[![App details contain your Sandbox and Live client ID and secrets](https://www.developerhelpline.com/wp-includes/images/get-client-id.jpg "App details contain your Sandbox and Live client ID and secrets")](https://www.developerhelpline.com/wp-includes/images/get-client-id.jpg "App details contain your Sandbox and Live client ID and secrets")

## Step 3 — Enable PayPal payments in mobile app

### Setup PayPal modules

To install **Paypal** plugin for Ionic, use

```javascript
$ ionic cordova plugin add com.paypal.cordova.mobilesdk

$ npm install @ionic-native/paypal
```

This will install PayPal plugin. Import **PayPal** into your component using

```javascript
import { PayPal, PayPalPayment, PayPalConfiguration } from '@ionic-native/paypal/ngx';
```

[![Import PayPal in home.page.ts file](https://www.developerhelpline.com/wp-includes/images/Import-PayPal-in-homepage-ts-file.jpg "Import PayPal in home.page.ts file")](https://www.developerhelpline.com/wp-includes/images/Import-PayPal-in-homepage-ts-file.jpg "Import PayPal in home.page.ts file")

You will also need to include `PayPal` in the list of providers in your `app.module.ts` file.

[![Import PayPal in your app.module.ts](https://www.developerhelpline.com/wp-includes/images/Import-PayPal-in-your-app-module-ts-file.jpg "Import PayPal in your app.module.ts")](https://www.developerhelpline.com/wp-includes/images/Import-PayPal-in-your-app-module-ts-file.jpg "Import PayPal in your app.module.ts")

### PayPal payment function

Invoke the payment function to initiate a payment. As mentioned in Step 2, You will require your `client_id` from your PayPal account. ([How to get my credentials from PayPal account](https://developer.paypal.com/docs/integration/direct/webhooks/my-apps-and-credentials/ "How to get my credentials from PayPal account")). This function will be attached to **Pay with PayPal** button we saw earlier in the app screenshot.

In the `payWithPaypal()` function, we will start by initializing the `PayPal` object with the PayPal environment (Sandbox or Production) to prepare the device for processing payments. Βy calling the `prepareToRender()` method we will pass the environment we set earlier. Finally, we will render the PayPal UI to collect the payment from the user by calling the `renderSinglePaymentUI()` method.

Complete `home.page.ts` file will look as follows:

```javascript
import { Component } from '@angular/core';
import { PayPal, PayPalPayment, PayPalConfiguration } from '@ionic-native/paypal/ngx';

@Component({
  selector: 'app-home',
  templateUrl: 'home.page.html',
  styleUrls: ['home.page.scss'],
})
export class HomePage {

  paymentAmount: string = '99.99';
  currency: string = 'USD';
  currencyIcon: string = '$';

  responseData: any = '';

  constructor(private payPal: PayPal) {}

  payWithPaypal() {
    this.payPal.init({
      PayPalEnvironmentProduction: 'YOUR_PRODUCTION_CLIENT_ID',
      PayPalEnvironmentSandbox: 'YOUR_SANDBOX_CLIENT_ID'
    }).then(() => {
      // Environments: PayPalEnvironmentNoNetwork, PayPalEnvironmentSandbox, PayPalEnvironmentProduction
      this.payPal.prepareToRender('PayPalEnvironmentSandbox', new PayPalConfiguration({
        // Only needed if you get an "Internal Service Error" after PayPal login!
        //payPalShippingAddressOption: 2 // PayPalShippingAddressOptionPayPal
      })).then(() => {
        let payment = new PayPalPayment(this.paymentAmount, this.currency, 'Description', 'sale');
        this.payPal.renderSinglePaymentUI(payment).then((res) => {
          this.responseData = JSON.stringify(res, null, 1);
          // Successfully paid

          // Example sandbox response
          //
          // {
          //   "client": {
          //     "environment": "sandbox",
          //     "product_name": "PayPal iOS SDK",
          //     "paypal_sdk_version": "2.16.0",
          //     "platform": "iOS"
          //   },
          //   "response_type": "payment",
          //   "response": {
          //     "id": "PAY-1AB23456CD789012EF34GHIJ",
          //     "state": "approved",
          //     "create_time": "2016-10-03T13:33:33Z",
          //     "intent": "sale"
          //   }
          // }
        }, () => {
          // Error or render dialog closed without being successful
        });
      }, () => {
        // Error in configuration
      });
    }, () => {
      // Error in initialization, maybe PayPal isn't supported or something else
    });
  }
}

```

Notice the `PayPalEnvironmentSandbox` parameter. This is used for Sandbox environment. For production environment, it will change to `PayPalEnvironmentProduction` . Of course, do not forget to replace `YOUR_SANDBOX_CLIENT_ID` with your Sandbox Client ID from **Step 2**.

Also notice, for the sake of a sample, we have taken `PaymentAmount` and `currency` as static in the logic, but these can be easily dynamic as per your app's requirement.

[![Static amount and currency for sample purpose](https://www.developerhelpline.com/wp-includes/images/Static-amount-and-currency-for-sample-purpose.jpg "Static amount and currency for sample purpose")](https://www.developerhelpline.com/wp-includes/images/Static-amount-and-currency-for-sample-purpose.jpg "Static amount and currency for sample purpose")

Once payment is done, PayPal SDK will return a response. A sample sandbox response is shown in the gist above. One can use this response to show appropriate *Toast* or *Alert* to app users, right now I'm showing the whole data JSON response.

[![Payment Response](https://www.developerhelpline.com/wp-includes/images/payment-response.jpg "Payment Response")](https://www.developerhelpline.com/wp-includes/images/payment-response.jpg "Payment Response")

Here's the HTML template for the `Ionic PayPal Integration App` homepage:

```javascript
<ion-content [fullscreen]="true">
  <ion-grid class="ion-no-padding">
    <ion-row class="ion-no-padding">
      <ion-col class="ion-margin-top ion-padding ion-text-center">
        Utilize this Pay button in your app's installment page with the connected rationale.
      </ion-col>
    </ion-row>
  </ion-grid>
  <ion-card class="welcome-card ion-margin">
    <ion-img src="./assets/paypal.jpg"></ion-img>
    <ion-card-header>
      <ion-card-subtitle>Get Started</ion-card-subtitle>
      <ion-card-title><b>PayPal Sample</b></ion-card-title>
      <ion-row>
        <ion-col style="padding-left: 0;">Total Payment</ion-col>
        <ion-col class="ion-text-end">
          {{currencyIcon}} {{paymentAmount}}
        </ion-col>
      </ion-row>
    </ion-card-header>
    <ion-card-content class="ion-no-padding">
      <ion-button expand="full" color="success" class="ion-no-margin" (click)="payWithPaypal()">Pay with PayPal</ion-button>
    </ion-card-content>
  </ion-card>

  <div *ngIf="responseData" class="ion-margin response ion-padding">
    <code>{{responseData}}
    </code>
  </div>

  <ion-list lines="none">
    <ion-list-header>
      <ion-label>Resources</ion-label>
    </ion-list-header>
    <ion-item href="https://ionicframework.com/docs/native/paypal" detail="true">
      <ion-icon slot="start" color="dark" name="book-outline"></ion-icon>
      <ion-label>Paypal Plugin Documentation</ion-label>
    </ion-item>
    <ion-item href="https://github.com/paypal/PayPal-Cordova-Plugin" detail="true">
      <ion-icon slot="start" color="dark" name="build-outline"></ion-icon>
      <ion-label>Paypal Plugin Repository</ion-label>
    </ion-item>
    <ion-item href="https://medium.com/enappd/ionic-4-paypal-payment-integration-for-apps-and-pwa-680b3f7ddb2f" detail="true">
      <ion-icon slot="start" color="dark" name="flash-outline"></ion-icon>
      <ion-label>Ionic 4 PayPal Payment Integration</ion-label>
    </ion-item>
    <ion-item href="https://www.developerhelpline.com/" detail="true">
      <ion-icon slot="start" src="./assets/developer-helpline-256.svg"></ion-icon>
      <ion-label>More on Developer Helpline</ion-label>
    </ion-item>
  </ion-list>
</ion-content>
```
