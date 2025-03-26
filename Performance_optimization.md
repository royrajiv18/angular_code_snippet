# Use OnPush change detection:

- This tells Angular to check for changes only when the component's inputs change instead of every event.

- import { ChangeDetectionStrategy, Component } from '@angular/core';

- @Component({
  selector: 'app-example',
  template: `<p>{{ data }}</p>`,
  changeDetection: ChangeDetectionStrategy.OnPush
  })
- export class ExampleComponent {
  @Input() data: string;
  }

  # Lazy Load Modules

  - {
    path: 'feature',
    loadChildren: ()=> import('./feature.module').then(m=> m.featureModule)
    }

# Use trackBy in \*ngFor to optimize rendering

- <li *ngFor="let item of items trackBy: trackByFn">{{item.name}}</li>

- trackByFn(index:number, item:any){
  return item.id // Unique identifier for each user
  }

# Use Pure Pipes Instead of Impure Pipes

- Ex-

  - @Pipe({
    name: 'capitalizePipe',
    pure: true
    })

  export class capitalizePipe implements PipeTransform{
  transform(value: string): string{
  return value.charAt(0).toUpperCase() + value.slice(1)
  }
  }

  # Use virtual scrolling for large lists

- <cdk-virtual-scroll-viewport itemSize="50" class="scroll-container">
    <div *cdkVirtualFor="let item of items">{{ item.name }}</div>
  </cdk-virtual-scroll-viewport>

# Use HttpClient with Caching

- Avoid making duplicate API calls.
- Ex -
  @Injecttable({
  providedIn: 'root'
  })

  export class DataService{
  constructor(private http: HttpClient){}

        private cache: any

        getData(): Observable<any>{
            if(this.cache){
                return of(this.cache)
            }
            return this.http.get('/api/data').pipe(
                tap(data=> this.cache=data)
            );
        }

  }

  # Use Angular CLI Flags for Production Build

  - ng build --configuration=production
    - Removes unused code (Tree Shaking)
    - Minifies JS and CSS
    - Enables Ahead-of-Time (AOT) Compilation

# Unsubscribe from Observables

# Use Web Workers for Heavy Computations

- worker.js - addEventListener('message', ({ data }) => {
  const result = heavyComputation(data);
  postMessage(result);
  });

- in ts file - const worker = new Worker('./worker.js');
  worker.postMessage(inputData);
  worker.onmessage = ({ data }) => console.log('Result:', data);

# Use Server-Side Rendering (SSR) with Angular Universal

- ng add @angular/universal

#
