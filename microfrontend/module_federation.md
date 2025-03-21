### Sharing dependency between micro frontends

##

Using Module Federation

- Step 1: Install Required Packages:
  - ng add @angular-architects/module-federation
- Step 2: Configure the Host and Remote Applications

  - Remote App: Modify webpack.config.js:

    - const { shareAll } = require('@angular-architects/module-federation/webpack');
      module.exports = {
      output: {
      uniqueName: 'remote1',
      publicPath: 'auto',
      },
      optimization: {
      runtimeChunk: false,
      },
      plugins: [
      new ModuleFederationPlugin({
      name: 'remote1',
      filename: 'remoteEntry.js',
      exposes: {
      './Component': './src/app/remote-component/remote.component.ts', // Exposing a component
      },
      shared: shareAll({ singleton: true, strictVersion: false, requiredVersion: 'auto' }),
      }),
      ],
      };

    - Host App
    - Modify webpack.config.js:

      - const { shareAll } = require('@angular-architects/module-federation/webpack');

        module.exports = {
        output: {
        uniqueName: 'host',
        publicPath: 'auto',
        },
        optimization: {
        runtimeChunk: false,
        },
        plugins: [
        new ModuleFederationPlugin({
        remotes: {
        remote1: 'remote1@http://localhost:4201/remoteEntry.js',
        },
        shared: shareAll({ singleton: true, strictVersion: false, requiredVersion: 'auto' }),
        }),
        ],
        };

Step 3: Ensure Dependencies are Shared in angular.json

- Modify angular.json for both apps: - "architect": {
  "build": {
  "options": {
  "allowedCommonJsDependencies": ["@angular/core", "@angular/common"]
  }
  }
  }
- This ensures that libraries like @angular/core and @angular/common are not bundled multiple times.

- Step 4: Load Remote Components in the Host
- Modify app.module.ts (Shell): - import { loadRemoteModule } from '@angular-architects/module-federation';
  import { Routes } from '@angular/router';

const routes: Routes = [
{
path: 'remote1',
loadChildren: () =>
loadRemoteModule({
remoteName: 'remote1',
exposedModule: './Component',
}).then((m) => m.RemoteComponent),
},
];
