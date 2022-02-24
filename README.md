# angular

<div *ngFor="let product of products">
</div>
*ngFor : sert à boucler dans le html, dans ce contexte particulier sert à boucler sur les produits.

La syntaxe {{ product.name }} ajoute la valeur de la proprieté product.name en tant que texte.

<p *ngIf="product.description">
    Description: {{ product.description }}
</p>  Avec ce code angular crée le paragraphe <p> si et seulement si le produit a une description.

<button type="button" (click)="share()">
    Share
</button> L'evenement click est attaché à la methode share(), cette methode est appelée chaque fois que l'on clique sur le bouton.

<p *ngIf="product && product.price > 700">
  <button type="button">Notify Me</button>
</p> Le bouton "Notify Me" apparait si product.price > 700.

<app-product-alerts
  [product]="product">
</app-product-alerts> création d'un composant product-alerts dans le html.

<p *ngIf="product && product.price > 700">
  <button type="button" (click)="notify.emit()">Notify Me</button>
</p> Au clic sur le bouton "Notify Me" la methode notify.emit() est appelée.
----------------------------------------------------------------
La deuxième partie(Adding navigation) consiste à parametrer les détails des produits en configurant les routes(url) pour chaque produit.

ng generate component product-details : permet de créer un composant product-details

RouterModule.forRoot([
      { path: '', component: ProductListComponent },
      { path: 'products/:productId', component: 
      permet de créer une route en ajoutant un path pour chaque composant.
[routerLink]="['/products', product.id]" : permet d'inclure une router link avec comme parametre product.id.

  product: Product | undefined; permet de définir la proprieté product.

  ------------------------------------------------------------
  Partie 3 : Managing Data

  ng generate service cart : permet de générer un service cart