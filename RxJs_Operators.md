### RxJs Operators

- of()

  - Create an Observable from static values
  - Use case - When you need to return mock data instead of an API call.
  - Ex -
    - import { of } from 'rxjs';
    - const numbers$ = of(1, 2, 3, 4, 5);
    - numbers$.subscribe(value => console.log(value)); // Output: 1, 2, 3, 4, 5

- from()
  - Convert array/promise to an Observable
  - Use Case: Convert an array, promise, or iterable into an Observable.
  - Ex -
    - import { from } from 'rxjs';
    - const array$ = from([10, 20, 30]);
    - array$.subscribe(value => console.log(value)); // Output: 10, 20, 30
  - Ex -
    - const promise$ = from(fetch('https://jsonplaceholder.typicode.com/todos/1'));
    - promise$.subscribe(response => console.log(response)); // Resolves and logs API response
- interval()

  - Emit values at a fixed interval
  - Use Case: Creating a countdown timer or auto-refresh mechanism.
  - Ex -
    - import { interval } from 'rxjs';
    - const timer$ = interval(1000);
    - timer$.subscribe(value => console.log(value)); // Emits 0, 1, 2... every second

- map()

  - Transform each emitted value
  - Use Case: Modify API responses before sending data to components.
  - Ex -
    - import { of } from 'rxjs';
    - import { map } from 'rxjs/operators';
    - of(1, 2, 3)
      - .pipe(map(value => value \* 10))
      - .subscribe(console.log); // Output: 10, 20, 30

- pluck()

  - Extract specific property from objects
  - Use Case: Extract only needed properties from API responses.
  - Ex -
    - import { from } from 'rxjs';
    - import { pluck } from 'rxjs/operators';
    - const users$ = from([{ name: 'John' }, { name: 'Jane' }]);
    - users$.pipe(pluck('name')).subscribe(console.log); // Output: "John", "Jane"

- switchMap()

  - Cancel previous request if a new one arrives
  - Use Case: Useful for search autocomplete, cancelling the previous HTTP request when the user types.
  - Ex -

    - import { fromEvent, of } from 'rxjs';
    - import { switchMap } from 'rxjs/operators';
    - const button = document.getElementById('btn');
    - const clicks$ = fromEvent(button, 'click');
    - clicks$
    - .pipe(switchMap(() => of('New API call started')))
    - .subscribe(console.log);

- filter()

  - Emit only values that match a condition
  - Use Case: Remove invalid form inputs before submission.
  - Ex -
    - import { of } from 'rxjs';
    - import { filter } from 'rxjs/operators';
    - of(1, 2, 3, 4, 5)
      - .pipe(filter(value => value % 2 === 0))
      - .subscribe(console.log); // Output: 2, 4

- debounceTime()

  - Ignore rapid emissions (Rate-Limiting)
  - Use Case: Search autocomplete to prevent frequent API calls.
    Ex -
    - import { fromEvent } from 'rxjs';
    - import { debounceTime } from 'rxjs/operators';
    - const searchBox = document.getElementById('search');
    - const keypress$ = fromEvent(searchBox, 'keyup');
    - keypress$
      - .pipe(debounceTime(500))
      - .subscribe(() => console.log('API Call made!'));

- distinctUntilChanged()

  - Emit values only when they change
  - Use Case: Avoid redundant API calls in a search input.
  - Ex -
    - import { from } from 'rxjs';
    - import { distinctUntilChanged } from 'rxjs/operators';
    - from([1, 1, 2, 2, 3, 3])
      - .pipe(distinctUntilChanged())
      - .subscribe(console.log); // Output: 1, 2, 3

- merge()

  - Merge multiple streams
  - Use Case: Combine click events from multiple buttons.
  - Ex -
    - import { merge, interval } from 'rxjs';
    - const obs1$ = interval(1000);
    - const obs2$ = interval(2000);
    - merge(obs1$, obs2$).subscribe(console.log);

- combineLatest()

  - Get the latest value from multiple observables
  - Use Case: Combine two dropdown selections dynamically.
  - Ex -
    - import { combineLatest, of } from 'rxjs';
    - const obs1$ = of('User1', 'User2');
    - const obs2$ = of('Admin', 'Editor');
    - combineLatest([obs1$, obs2$]).subscribe(console.log);
    - // Output: ['User1', 'Admin'], ['User2', 'Editor']

- catchError()

  - Handle errors and return fallback
  - Use Case: Provide a fallback response when an API call fails.

- retry()

  - Retry an operation on failure
  - Use Case: Retry API requests if they fail due to network issues.

- tap()

  - Perform side-effects without modifying data
  - Use Case: Debugging API responses before passing data to components.

- delay()
  - Delay emission of values
  -
