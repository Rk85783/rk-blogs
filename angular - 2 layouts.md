Agar aap **Angular me 2 alag header aur footer** implement karna chahte hain—  
✅ **Ek header/footer**: Home, About, Contact, Blog pages ke liye  
✅ **Dusra header/footer**: Admin Dashboard, Blog Add, List, Delete, View ke liye  

To aap **Layout-Based Routing Approach** use kar sakte hain. Isme alag-alag layouts (`components`) create karke unko `RouterOutlet` ke saath set karenge.

---

## **🚀 Steps to Implement**
1. **Do alag layout components banayein**  
   - `MainLayoutComponent` → Public pages ke liye (Home, About, Contact, Blog)  
   - `AdminLayoutComponent` → Admin pages ke liye (Dashboard, Blog Add, List, etc.)  
   
2. **Headers aur Footers ko layouts ke andar rakhein.**  
3. **App Routing me layouts ko setup karein.**

---

## **📌 1. Folder Structure**
```
src/
│── app/
│   │── layouts/
│   │   │── main-layout/
│   │   │   ├── main-layout.component.ts
│   │   │   ├── main-layout.component.html
│   │   │   ├── main-layout.component.css
│   │   │
│   │   │── admin-layout/
│   │   │   ├── admin-layout.component.ts
│   │   │   ├── admin-layout.component.html
│   │   │   ├── admin-layout.component.css
│   │
│   │── components/
│   │   │── header-main.component.ts
│   │   │── footer-main.component.ts
│   │   │── header-admin.component.ts
│   │   │── footer-admin.component.ts
│   │
│   │── pages/
│   │   │── home.component.ts
│   │   │── about.component.ts
│   │   │── contact.component.ts
│   │   │── blog.component.ts
│   │   │── admin-dashboard.component.ts
│   │   │── blog-add.component.ts
│   │   │── blog-list.component.ts
│   │   │── blog-delete.component.ts
│   │   │── blog-view.component.ts
│
│── app-routing.module.ts
│── app.module.ts
```

---

## **📌 2. Layout Components**
### **➡️ `MainLayoutComponent` (Public Pages)**
#### **📄 main-layout.component.html**
```html
<app-header-main></app-header-main>  <!-- Public Header -->
<router-outlet></router-outlet>       <!-- Page Content -->
<app-footer-main></app-footer-main>  <!-- Public Footer -->
```

#### **📄 main-layout.component.ts**
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-main-layout',
  templateUrl: './main-layout.component.html',
  styleUrls: ['./main-layout.component.css']
})
export class MainLayoutComponent {}
```

---

### **➡️ `AdminLayoutComponent` (Admin Pages)**
#### **📄 admin-layout.component.html**
```html
<app-header-admin></app-header-admin>  <!-- Admin Header -->
<router-outlet></router-outlet>         <!-- Admin Content -->
<app-footer-admin></app-footer-admin>  <!-- Admin Footer -->
```

#### **📄 admin-layout.component.ts**
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-admin-layout',
  templateUrl: './admin-layout.component.html',
  styleUrls: ['./admin-layout.component.css']
})
export class AdminLayoutComponent {}
```

---

## **📌 3. Header & Footer Components**
### **➡️ Public Header (`header-main.component.html`)**
```html
<nav>
  <a routerLink="/home">Home</a>
  <a routerLink="/about">About</a>
  <a routerLink="/contact">Contact</a>
  <a routerLink="/blog">Blog</a>
</nav>
```

### **➡️ Admin Header (`header-admin.component.html`)**
```html
<nav>
  <a routerLink="/admin/dashboard">Dashboard</a>
  <a routerLink="/admin/blog/add">Add Blog</a>
  <a routerLink="/admin/blog/list">Blog List</a>
</nav>
```

---

## **📌 4. Routing Module Setup**
#### **📄 app-routing.module.ts**
```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { MainLayoutComponent } from './layouts/main-layout/main-layout.component';
import { AdminLayoutComponent } from './layouts/admin-layout/admin-layout.component';
import { HomeComponent } from './pages/home.component';
import { AboutComponent } from './pages/about.component';
import { ContactComponent } from './pages/contact.component';
import { BlogComponent } from './pages/blog.component';
import { AdminDashboardComponent } from './pages/admin-dashboard.component';
import { BlogAddComponent } from './pages/blog-add.component';
import { BlogListComponent } from './pages/blog-list.component';
import { BlogDeleteComponent } from './pages/blog-delete.component';
import { BlogViewComponent } from './pages/blog-view.component';

const routes: Routes = [
  {
    path: '',
    component: MainLayoutComponent,
    children: [
      { path: 'home', component: HomeComponent },
      { path: 'about', component: AboutComponent },
      { path: 'contact', component: ContactComponent },
      { path: 'blog', component: BlogComponent },
      { path: '', redirectTo: 'home', pathMatch: 'full' }
    ]
  },
  {
    path: 'admin',
    component: AdminLayoutComponent,
    children: [
      { path: 'dashboard', component: AdminDashboardComponent },
      { path: 'blog/add', component: BlogAddComponent },
      { path: 'blog/list', component: BlogListComponent },
      { path: 'blog/delete', component: BlogDeleteComponent },
      { path: 'blog/view', component: BlogViewComponent },
      { path: '', redirectTo: 'dashboard', pathMatch: 'full' }
    ]
  },
  { path: '**', redirectTo: 'home' }  // Not found page redirect
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

---

## **📌 5. Module Configuration**
#### **📄 app.module.ts**
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

// Layouts
import { MainLayoutComponent } from './layouts/main-layout/main-layout.component';
import { AdminLayoutComponent } from './layouts/admin-layout/admin-layout.component';

// Components
import { HeaderMainComponent } from './components/header-main.component';
import { FooterMainComponent } from './components/footer-main.component';
import { HeaderAdminComponent } from './components/header-admin.component';
import { FooterAdminComponent } from './components/footer-admin.component';

// Pages
import { HomeComponent } from './pages/home.component';
import { AboutComponent } from './pages/about.component';
import { ContactComponent } from './pages/contact.component';
import { BlogComponent } from './pages/blog.component';
import { AdminDashboardComponent } from './pages/admin-dashboard.component';
import { BlogAddComponent } from './pages/blog-add.component';
import { BlogListComponent } from './pages/blog-list.component';
import { BlogDeleteComponent } from './pages/blog-delete.component';
import { BlogViewComponent } from './pages/blog-view.component';

@NgModule({
  declarations: [
    AppComponent,
    MainLayoutComponent,
    AdminLayoutComponent,
    HeaderMainComponent,
    FooterMainComponent,
    HeaderAdminComponent,
    FooterAdminComponent,
    HomeComponent,
    AboutComponent,
    ContactComponent,
    BlogComponent,
    AdminDashboardComponent,
    BlogAddComponent,
    BlogListComponent,
    BlogDeleteComponent,
    BlogViewComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

---

## **🎯 Final Output**
✅ **Public Pages** (Home, About, Contact, Blog) → `MainLayoutComponent` with Public Header/Footer  
✅ **Admin Pages** (Dashboard, Blog Add, List, etc.) → `AdminLayoutComponent` with Admin Header/Footer  
✅ **Alag-alag header/footer automatically switch honge based on route!** 🎉  

Agar koi aur customization chahiye ho to batao! 🚀😃
