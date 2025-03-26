# Forms - Template and Reactive

# Template uses ngModel

- <input [(ngModel)]="name">

# Reactive Forms uses FormControl and FormGroup

- this.form = new FormGroup({
  name: new FormControl('')
  })
