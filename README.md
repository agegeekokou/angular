# angular
```html
<div *ngFor="let product of products">
</div>
```
*ngFor : sert à boucler dans le html, dans ce contexte particulier sert à boucler sur les products.

La syntaxe {{ product.name }} ajoute la valeur de la proprieté product.name en tant que texte.

```html
<p *ngIf="product.description">
    Description: {{ product.description }}
</p> 
```
 Avec ce code angular crée le paragraphe <p> si et seulement si le produit a une description.

```html
<button type="button" (click)="share()">
    Share
</button>
```
 L'evenement click est attaché à la methode share(), cette methode est appelée chaque fois que l'on clique sur le bouton.

```html
<p *ngIf="product && product.price > 700">
  <button type="button">Notify Me</button>
</p> 
```

Le bouton "Notify Me" apparait si product.price > 700.

```ts
<app-product-alerts
  [product]="product">
</app-product-alerts> 
```
création d'un composant product-alerts dans le html.

```html
<p *ngIf="product && product.price > 700">
  <button type="button" (click)="notify.emit()">Notify Me</button>
</p>
``` 
Au clic sur le bouton "Notify Me" la methode notify.emit() est appelée.
----------------------------------------------------------------
Partie 2

La deuxième partie(Adding navigation) consiste à parametrer les détails des produits en configurant les routes(url) pour chaque produit.

ng generate component product-details : permet de créer un composant product-details

```ts
RouterModule.forRoot([
      { path: '', component: ProductListComponent },
      { path: 'products/:productId', component}: 
```
      permet de créer une route en ajoutant un path pour chaque composant.

```ts
[routerLink]="['/products', product.id]"
```
: permet d'inclure une router link avec comme parametre product.id.

```
```ts
  product: Product | undefined; 
```
  : permet de définir la proprieté product.

  ------------------------------------------------------------
  Partie 3 : Managing Data

  ng generate service cart : permet de générer un service cart

```ts
  export class CartService {
  items: Product[] = [];
/* . . . */
}
``` 
: Ce code permet de stocker le tableau du produit actuel dans la cart.

```ts
addToCart(product: Product) {
    this.items.push(product);
  }
  ``` 
  : Cette methode permet d'ajouter un item à la cart. Elle permet d'ajouter un item au tableau d'items.

```ts
  getItems() {
    return this.items;
  }
  ``` 
  : Cette methode retourne l'item de la cart.

```ts
  clearCart() {
    this.items = [];
    return this.items;
  }
  ```
   : Cette methode permet de supprimer un item de la cart.
  Elle retourne un tableau vide de la cart.

```ts
  constructor(
    private route: ActivatedRoute,
    private cartService: CartService
  ) { }
  ```
   : Injection de la cart service en l'ajoutant au constructeur.

```ts
  addToCart(product: Product) {
    this.cartService.addToCart(product);
    window.alert('Your product has been added to the cart!');
  }
``` 
  : Cette methode ajoute le product actuel à la cart.

```html
  <div *ngIf="product">
  <h3>{{ product.name }}</h3>
  <h4>{{ product.price | currency }}</h4>
  <p>{{ product.description }}</p>
  <button type="button" (click)="addToCart(product)">Buy</button>
</div>
```
 : Si le produit existe, le nom, le prix et la description du product sont affichés. Un evenement click est attaché au bouton Buy et la methode addToCard() est appelée. Elle ajoute le product à la cart en le prenant en paramètre.


```ts
constructor(
    private cartService: CartService
  ) { }
}
``` 
: permet d'ajouter le cart service au constructeur


```ts
 items = this.cartService.getItems(); 
 ```
 :  permet de définir la proprieté items pour stocker product dans la cart.


```html
 <div class="cart-item" *ngFor="let item of items">
  <span>{{ item.name }}</span>
  <span>{{ item.price | currency }}</span>
</div> 
```
: Template dans lequel la boucle for parcours et affiche chaque item avec son nom et son prix.

```ts
shippingCosts = this.cartService.getShippingPrices();
```
Définition de la proprieté shippingCosts qui utilise la methode getShippingPrices() de cartService.

--------------------------------------------------------------
Partie 4
La partie 4 consiste à programmer un formulaire pour le composant cart.

```ts
import { FormBuilder } from '@angular/forms';
```
: Pour ce faire, on importe tout d'abord le FormBuilder service du package @angular/forms

```ts
constructor(
    private cartService: CartService,
    private formBuilder: FormBuilder,
  ) {}
```
 : On injecte le FormBuilder service dans le constructeur de CartComponent

 ```ts
 checkoutForm = this.formBuilder.group({
    name: '',
    address: ''
  });
```
 : Cette methode permet de recueillir les noms et adresses des utilisateurs et de les mettre dans des champs nom et adresse.

 ```ts
 onSubmit(): void {
    // Process checkout data here
    this.items = this.cartService.clearCart();
    console.warn('Your order has been submitted', this.checkoutForm.value);
    this.checkoutForm.reset();
  }
```
 : Cette methode autorise les utilisateurs à soumettre leur noms et adresses. Elle utilise la methode clearCart() du CartService pour réinitialiser le formulaire et effacer la cart.

 ```html
 <form [formGroup]="checkoutForm">

  <button class="button" type="submit">Purchase</button>

</form>
```
 : Ajout du formulaire checkoutForm et du bouton Purchasse.

 ```html
 <form [formGroup]="checkoutForm" (ngSubmit)="onSubmit()">
</form>
```
 : Création d'un evenement ngSubmit sur le formulaire checkoutForm. A la soumission du formulaire la methode 
 onSubmit() est appelée.

 ```html
 <div>
    <label for="name">
      Name
    </label>
    <input id="name" type="text" formControlName="name">
  </div>

  <div>
    <label for="address">
      Address
    </label>
    <input id="address" type="text" formControlName="address">
  </div>
```
 : Ajout de champ input et de label name et adress.

