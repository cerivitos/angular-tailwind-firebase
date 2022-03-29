 <p align="center">🔥🔥🔥</p>
 <h1 align="center">Angular-Tailwind-Firebase Starter Template</h1>


###



This is a starter template with my commonly used dependencies for building web apps with Angular v13.    



## Tailwind

[Tailwind CSS v3](https://tailwindcss.com) is set up with the `line-clamp` plugin which is useful to control text in fixed dimension containers.

## Firebase

Start by [creating](https://firebase.com) a Firebase web project and copy the config object to `environment.ts`.

```
 firestoreConfig: {
    apiKey: '<your-key>',
    authDomain: '<your-project-authdomain>',
    databaseURL: '<your-database-URL>',
    projectId: '<your-project-id>',
    storageBucket: '<your-storage-bucket>',
    messagingSenderId: '<your-messaging-sender-id>',
  },
 ```
 
Tip: Do check out [ReCaptcha v3](https://www.google.com/recaptcha/about) which is really useful for Firestore/Real Time Database security. Unfortunately implementation in Angular is not very well documented. Usually, I implement the ReCaptcha check in a Service which handles my calls to Firebase.

```
...
import {
  initializeAppCheck,
  ReCaptchaV3Provider,
} from '@angular/fire/app-check';
...

@Injectable({
  providedIn: 'root',
})
export class DataService {
  constructor(
    private firestore: AngularFirestore,
    private http: HttpClient
  ) {
    initializeAppCheck(getApp(), {
      provider: new ReCaptchaV3Provider(environment.appCheckKey),
      isTokenAutoRefreshEnabled: true,
    });
  }
 ...
}
```

Remember to include your [unique App Check key](https://firebase.google.com/docs/app-check/web/recaptcha-provider) from ReCaptcha v3 in Firebase Settings.

## Vercel Serverless Functions

I usually use [Vercel](https://vercel.com) for hosting. Vercel allows you to create serverless functions simply by creating an exported function in the `/api` folder. For example, this function will return 'Hello World!' at the end point `https://your-app.vercel.app/api/query` when hosted on Vercel.

**api/query.ts**
```
import type { VercelRequest, VercelResponse } from '@vercel/node';

export default (req: VercelRequest, res: VercelResponse) => {
  res.status(200).send('Hello World!);
};
```

Types for Vercel functions are already included.

## Miscellaneous

[Web APIs for Angular](https://github.com/ng-web-apis/common) are included. This provides useful injection tokens to access common Web APIs. For example, `WINDOW` allows access to the global `window` object.

My go-to toast library is [Hot Toast](https://github.com/ngneat/hot-toast).

## License
MIT (2022)
