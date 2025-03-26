# Directives are used to extend the functionality of elements

- Structural Directives (*ngIf, *ngFor, \*ngSwitch): Modify DOM elements.
- Attribute Directives ([ngClass], [ngStyle]): Modify element appearance
- Ex
- <p *ngIf="isLoggedIn">Welcome back!</p>
- <ul>
  - <li *ngFor="let item of items">{{ item }}</li>
- </ul>

- Custom Directives: Created using @Directive()
