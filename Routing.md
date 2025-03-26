# Routing - Angular Router enables navigation between different views.

- AppRouting module
- Ex -
  const routes: Routes = [
  {
  path: 'home',
  component: HomeComponent
  },
  {
  path: 'about',
  component: AboutComponent
  },
  {
  path: '**',
  redirectTo: 'home'
  },
  ]

  @ngModules({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
  })

  export class AppRoutingModule {}

  - Usage -
    <a routerLink = "/home">Home</a>
    <router-outlet></router-outlet>
