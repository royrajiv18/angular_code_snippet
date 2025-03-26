# Services - Services are used for sharing data and logic across components (e.g., API calls, logging, authentication).

- Ex -
- @Injectable({
  providedIn: 'root'
  })

export class UserService {
constructor(private http: HttpClient){}
getUsers(){
return this.http.get('https://api.example.com/users')
}
}
