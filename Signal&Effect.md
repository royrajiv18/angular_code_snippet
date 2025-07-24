Signal - A reactive primitive that holds a value and notifies dependents when the value changes.
Effects - A reactive side effect that runs automatically when any of the signals it depends on change.

Ex - 
import { Component, signal, effect } from '@angular/core';

@Component({
  selector: 'app-counter',
  template: `
    <h2>Counter: {{ count() }}</h2>
    <button (click)="increment()">Increment</button>
  `,
})
export class CounterComponent {
  count = signal(0); // ✅ define signal

  constructor() {
    effect(() => {
      console.log('Count changed:', this.count()); // ✅ effect watches signal
    });
  }

  increment() {
    this.count.set(this.count() + 1);
  }
}

