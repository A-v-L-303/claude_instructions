# Angular 21.1.0 + Bootstrap 5.3 – HTML Guide for LLMs

## Meta
- Angular version: 21.1.0
- Bootstrap version: 5.3.x
- ng-bootstrap version: 20.x (minimum requirement: Angular 21.0.0)
- All components: standalone (no NgModules required)
- Template syntax: modern control flow (@if, @for, @switch)
- No jQuery; Bootstrap 5 is jQuery-free

---

## 1. Installation

### 1a. Bootstrap CSS only (no JS-components needed)

```bash
npm install bootstrap
```

`angular.json` → `projects.<name>.architect.build.options`:

```json
"styles": [
  "node_modules/bootstrap/dist/css/bootstrap.min.css",
  "src/styles.scss"
],
"scripts": []
```

If SCSS customization is needed, import in `styles.scss` instead:

```scss
// Optional: override variables BEFORE import
$primary: #3498db;

@import "bootstrap/scss/bootstrap";
```

Partial imports (performance):

```scss
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/grid";
@import "bootstrap/scss/utilities";
@import "bootstrap/scss/buttons";
// add only what you need
```

### 1b. With Bootstrap JavaScript components (modals, dropdowns, tooltips)

**DO NOT use Bootstrap's JS directly with Angular.**  
Use `ng-bootstrap` instead — it provides Angular-native components with no jQuery.

```bash
ng add @ng-bootstrap/ng-bootstrap
```

Or manual:

```bash
npm install @ng-bootstrap/ng-bootstrap @popperjs/core
```

### 1c. Component entry points (ng-bootstrap 20.x feature)

ng-bootstrap 20.x supports per-component imports for smaller bundles:

```typescript
import { NgbPagination } from '@ng-bootstrap/ng-bootstrap/pagination';
import { NgbModal }      from '@ng-bootstrap/ng-bootstrap/modal';
import { NgbDropdown }   from '@ng-bootstrap/ng-bootstrap/dropdown';
// etc.
```

Main entrypoint still works (no breaking change):

```typescript
import { NgbPaginationModule, NgbModalModule } from '@ng-bootstrap/ng-bootstrap';
```

---

## 2. Angular 21 Template Syntax Rules

Angular 21 uses **standalone components by default**. Import Bootstrap-related directives directly in the `imports` array of each component.

### 2a. Standalone component skeleton

```typescript
import { Component } from '@angular/core';
import { NgbAlert } from '@ng-bootstrap/ng-bootstrap/alert';

@Component({
  selector: 'app-example',
  standalone: true,
  imports: [NgbAlert],
  template: `
    <ngb-alert type="success">Operation successful.</ngb-alert>
  `
})
export class ExampleComponent {}
```

### 2b. Control flow (replaces *ngIf / *ngFor)

```html
@if (isLoggedIn) {
  <div class="alert alert-success">Welcome back!</div>
} @else {
  <div class="alert alert-warning">Please log in.</div>
}

@for (item of items; track item.id) {
  <div class="list-group-item">{{ item.name }}</div>
}

@switch (status) {
  @case ('active') { <span class="badge bg-success">Active</span> }
  @case ('inactive') { <span class="badge bg-secondary">Inactive</span> }
  @default { <span class="badge bg-warning">Unknown</span> }
}
```

### 2c. Signals in templates

```typescript
import { signal, computed } from '@angular/core';

count = signal(0);
doubled = computed(() => this.count() * 2);
```

```html
<p class="text-muted">Count: {{ count() }}</p>
<button class="btn btn-primary" (click)="count.set(count() + 1)">Increment</button>
```

---

## 3. Bootstrap Grid System

Bootstrap uses a 12-column flexbox grid. Breakpoints: `xs` (default, <576px), `sm` (≥576px), `md` (≥768px), `lg` (≥992px), `xl` (≥1200px), `xxl` (≥1400px).

### Basic grid

```html
<div class="container">
  <div class="row">
    <div class="col-md-4">Column 1</div>
    <div class="col-md-4">Column 2</div>
    <div class="col-md-4">Column 3</div>
  </div>
</div>
```

### Responsive columns

```html
<div class="container-fluid">
  <div class="row g-3">
    <div class="col-12 col-sm-6 col-lg-4">
      <div class="card h-100">
        <div class="card-body">Content</div>
      </div>
    </div>
  </div>
</div>
```

- `g-3` = gutter spacing (gap between columns/rows)
- `container` = fixed-width centered; `container-fluid` = full-width

---

## 4. Bootstrap CSS Classes – Quick Reference

### Typography

| Class | Effect |
|---|---|
| `text-primary` / `text-secondary` | Brand colors |
| `text-muted` | Gray text |
| `fw-bold` / `fw-light` | Font weight |
| `fs-1` … `fs-6` | Font size scale |
| `lead` | Large intro text |
| `text-truncate` | Truncate with ellipsis |

### Spacing (margin/padding)

Pattern: `{property}{side}-{breakpoint}-{size}`  
Property: `m` (margin) / `p` (padding)  
Side: `t` top, `b` bottom, `s` start, `e` end, `x` horizontal, `y` vertical  
Size: 0–5, `auto`

```html
<div class="mt-3 mb-4 px-2 py-lg-5">...</div>
```

### Display & Flexbox

```html
<div class="d-flex justify-content-between align-items-center gap-2">
  <span>Left</span>
  <span>Right</span>
</div>

<div class="d-none d-md-block">Visible only ≥md</div>
```

---

## 5. Bootstrap Components in Pure HTML (CSS-only, no JS)

These work with Bootstrap CSS alone — no ng-bootstrap required.

### Alerts

```html
<div class="alert alert-danger alert-dismissible fade show" role="alert">
  An error occurred.
  <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
</div>
```

**Note:** `data-bs-dismiss` requires Bootstrap JS. For Angular, use ng-bootstrap `<ngb-alert>` or handle dismissal via component state.

### Badges

```html
<span class="badge bg-primary">New</span>
<span class="badge bg-success rounded-pill">42</span>
```

### Cards

```html
<div class="card shadow-sm">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Title</h5>
    <p class="card-text text-muted">Description text.</p>
    <a href="#" class="btn btn-primary">Action</a>
  </div>
  <div class="card-footer text-muted">Footer</div>
</div>
```

### Buttons

```html
<button class="btn btn-primary">Primary</button>
<button class="btn btn-outline-secondary">Outline</button>
<button class="btn btn-danger btn-sm">Small Danger</button>
<button class="btn btn-success btn-lg w-100">Full Width</button>
<button class="btn btn-primary" disabled>Disabled</button>
```

### Forms

```html
<form>
  <div class="mb-3">
    <label for="email" class="form-label">Email</label>
    <input type="email" class="form-control" id="email" placeholder="name@example.com">
    <div class="form-text">We'll never share your email.</div>
  </div>
  <div class="mb-3">
    <label for="pwd" class="form-label">Password</label>
    <input type="password" class="form-control is-invalid" id="pwd">
    <div class="invalid-feedback">Please enter a valid password.</div>
  </div>
  <div class="form-check mb-3">
    <input class="form-check-input" type="checkbox" id="agree">
    <label class="form-check-label" for="agree">I agree</label>
  </div>
  <button class="btn btn-primary" type="submit">Submit</button>
</form>
```

Validation state classes: `is-valid` / `is-invalid` on `form-control`.

### Tables

```html
<table class="table table-striped table-hover table-bordered table-sm">
  <thead class="table-dark">
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1</th>
      <td>Alice</td>
      <td><span class="badge bg-success">Active</span></td>
    </tr>
  </tbody>
</table>
```

Responsive table: wrap in `<div class="table-responsive">`.

### List Group

```html
<ul class="list-group">
  <li class="list-group-item active">Active item</li>
  <li class="list-group-item">Second item</li>
  <li class="list-group-item list-group-item-danger">Danger item</li>
</ul>
```

### Progress

```html
<div class="progress" style="height: 20px;">
  <div class="progress-bar bg-success" role="progressbar"
       style="width: 65%;" aria-valuenow="65" aria-valuemin="0" aria-valuemax="100">
    65%
  </div>
</div>
```

### Spinners

```html
<div class="spinner-border text-primary" role="status">
  <span class="visually-hidden">Loading...</span>
</div>

<div class="spinner-grow text-secondary" role="status">
  <span class="visually-hidden">Loading...</span>
</div>
```

---

## 6. ng-bootstrap Components (JS-dependent, Angular-native)

These replace Bootstrap's JavaScript-powered components. Import per component entry point or from main entrypoint.

### Modal

```typescript
import { Component } from '@angular/core';
import { NgbModal } from '@ng-bootstrap/ng-bootstrap/modal';

@Component({
  selector: 'app-modal-demo',
  standalone: true,
  template: `
    <button class="btn btn-primary" (click)="open(content)">Open Modal</button>

    <ng-template #content let-modal>
      <div class="modal-header">
        <h4 class="modal-title">Modal Title</h4>
        <button type="button" class="btn-close" (click)="modal.dismiss()"></button>
      </div>
      <div class="modal-body">
        <p>Modal content here.</p>
      </div>
      <div class="modal-footer">
        <button class="btn btn-secondary" (click)="modal.dismiss()">Cancel</button>
        <button class="btn btn-primary" (click)="modal.close('confirm')">Confirm</button>
      </div>
    </ng-template>
  `
})
export class ModalDemoComponent {
  constructor(private modalService: NgbModal) {}

  open(content: any) {
    this.modalService.open(content, { size: 'lg', centered: true });
  }
}
```

### Dropdown

```typescript
import { NgbDropdownModule } from '@ng-bootstrap/ng-bootstrap/dropdown';
```

```html
<div ngbDropdown class="d-inline-block">
  <button class="btn btn-outline-primary" ngbDropdownToggle>Options</button>
  <div ngbDropdownMenu>
    <button ngbDropdownItem>Action 1</button>
    <button ngbDropdownItem>Action 2</button>
    <div class="dropdown-divider"></div>
    <button ngbDropdownItem class="text-danger">Delete</button>
  </div>
</div>
```

### Pagination

```typescript
import { NgbPagination } from '@ng-bootstrap/ng-bootstrap/pagination';
```

```html
<ngb-pagination
  [collectionSize]="totalItems"
  [(page)]="currentPage"
  [pageSize]="itemsPerPage"
  [maxSize]="5"
  [rotate]="true"
  [boundaryLinks]="true">
</ngb-pagination>
```

### Tooltip

```typescript
import { NgbTooltipModule } from '@ng-bootstrap/ng-bootstrap/tooltip';
```

```html
<button class="btn btn-secondary"
        ngbTooltip="Tooltip text here"
        placement="top">
  Hover me
</button>
```

### Accordion (directive-based, ng-bootstrap 14+)

```typescript
import { NgbAccordionModule } from '@ng-bootstrap/ng-bootstrap/accordion';
```

```html
<div ngbAccordion>
  <div ngbAccordionItem>
    <h2 ngbAccordionHeader>
      <button ngbAccordionButton>Section 1</button>
    </h2>
    <div ngbAccordionCollapse>
      <div ngbAccordionBody>
        <ng-template>Content of section 1</ng-template>
      </div>
    </div>
  </div>
</div>
```

---

## 7. Navbar

Pure Bootstrap CSS navbar (no JS toggler needed for simple cases):

```html
<nav class="navbar navbar-expand-lg bg-dark navbar-dark px-3">
  <a class="navbar-brand" href="#">MyApp</a>
  <button class="navbar-toggler" type="button"
          data-bs-toggle="collapse" data-bs-target="#mainNav">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="mainNav">
    <ul class="navbar-nav ms-auto">
      <li class="nav-item">
        <a class="nav-link active" routerLink="/">Home</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" routerLink="/about">About</a>
      </li>
    </ul>
  </div>
</nav>
```

**Note:** `data-bs-toggle` / `data-bs-target` require Bootstrap JS. For Angular SSR or CSP-strict projects, control collapse state via Angular component logic:

```typescript
isNavCollapsed = signal(true);
```

```html
<div [class.collapse]="isNavCollapsed()" class="navbar-collapse" id="mainNav">
  ...
</div>
<button class="navbar-toggler" (click)="isNavCollapsed.set(!isNavCollapsed())">
  <span class="navbar-toggler-icon"></span>
</button>
```

---

## 8. Angular Reactive Forms + Bootstrap Validation

```typescript
import { Component } from '@angular/core';
import { ReactiveFormsModule, FormBuilder, Validators } from '@angular/forms';

@Component({
  selector: 'app-form',
  standalone: true,
  imports: [ReactiveFormsModule],
  template: `
    <form [formGroup]="form" (ngSubmit)="submit()" novalidate>
      <div class="mb-3">
        <label class="form-label">Email</label>
        <input formControlName="email" type="email"
               class="form-control"
               [class.is-invalid]="form.get('email')?.invalid && form.get('email')?.touched">
        <div class="invalid-feedback">Valid email required.</div>
      </div>
      <button class="btn btn-primary" type="submit" [disabled]="form.invalid">
        Submit
      </button>
    </form>
  `
})
export class FormComponent {
  form = this.fb.group({
    email: ['', [Validators.required, Validators.email]]
  });

  constructor(private fb: FormBuilder) {}

  submit() { console.log(this.form.value); }
}
```

---

## 9. Dark Mode

Bootstrap 5.3 supports built-in dark mode via the `data-bs-theme` attribute.

```html
<!-- Apply to root element -->
<html data-bs-theme="dark">

<!-- Or per component -->
<div data-bs-theme="dark" class="card p-3">
  Dark card
</div>
```

Toggle dynamically in Angular:

```typescript
theme = signal<'light' | 'dark'>('light');
toggleTheme() { this.theme.set(this.theme() === 'light' ? 'dark' : 'light'); }
```

```html
<body [attr.data-bs-theme]="theme()">
  <button class="btn btn-outline-secondary" (click)="toggleTheme()">Toggle Theme</button>
</body>
```

---

## 10. Bootstrap Utilities – Frequently Used

```html
<!-- Shadows -->
<div class="shadow-sm">slight shadow</div>
<div class="shadow">normal shadow</div>
<div class="shadow-lg">large shadow</div>

<!-- Border -->
<div class="border border-primary rounded-3 p-3">Rounded box</div>

<!-- Position -->
<div class="position-relative">
  <span class="position-absolute top-0 end-0 badge bg-danger">99+</span>
</div>

<!-- Overflow -->
<div class="overflow-auto" style="max-height: 200px;">scrollable content</div>

<!-- Visibility -->
<span class="visually-hidden">screen reader only</span>
<div class="invisible">takes space, not visible</div>

<!-- Z-index -->
<div class="z-1">z-index: 1</div>
```

---

## 11. SSR / Hydration Considerations

Angular 21 supports SSR and hydration by default.

- ng-bootstrap 20.x components are fully hydratable.
- Components using i18n require `withI18nSupport()` (experimental).
- Avoid `document`/`window` access inside Bootstrap JS calls during SSR — use ng-bootstrap directives instead.
- `data-bs-*` attributes that trigger Bootstrap JS will not work during SSR; Angular-native alternatives (ng-bootstrap directives, signal-based state) are always preferred.

---

## 12. CSP (Content Security Policy)

Bootstrap 5 supports CSP mode:
- Use `data-bs-*` attributes instead of inline JS.
- Prefer ng-bootstrap for modal/dropdown/tooltip — it emits no inline scripts.
- Do not use `eval()` or `unsafe-inline` in scripts.

---

## 13. Version Compatibility Summary

| ng-bootstrap | Angular | Bootstrap CSS |
|---|---|---|
| 20.x | ≥21.0.0 | 5.3.x |
| 19.x | ≥19.0.0 | 5.3.x |
| 18.x (17.x) | ≥18.0.0 | 5.3.x |
| 17.x | ≥17.0.0 | 5.3.x |

---

## 14. Pitfalls

1. **Do not import NgModule-based APIs** — Angular 21 default projects are standalone-only. Use standalone imports array.
2. **Do not use Bootstrap.js + Angular together** — jQuery-based Bootstrap components conflict with Angular's change detection. Use ng-bootstrap.
3. **Do not use `*ngIf` / `*ngFor`** in new code — use `@if` / `@for` control flow blocks.
4. **Do not add styles inside component `styles` array for Bootstrap** — add to global `styles.scss` or `angular.json` styles array. Bootstrap CSS is global, not scoped.
5. **`data-bs-dismiss` on modals/alerts requires Bootstrap JS** — replace with Angular event binding + component state.
6. **ng-bootstrap 20.x requires Angular 21 minimum** — do not use older ng-bootstrap versions with Angular 21 (peer dependency conflicts).
