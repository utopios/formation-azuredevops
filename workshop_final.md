# Workshop : Développement et gestion d'une application ASP.NET Core MVC avec Azure DevOps

## Objectif

Créer un système de suivi des incidents pour un service public, tout en se focalisant sur les pratiques agiles et l'utilisation d'Azure Boards pour gérer le projet, et sur Azure Pipelines pour l'intégration et le déploiement continu.


## 1. Planification dans Azure Boards

### 1.1 Épics et issues

#### Epic 1 : Signalement des incidents
- **Issue 1.1 : Formulaire de signalement**
- **Issue 1.2 : Validation des données**
- **Issue 1.3 : Persistance des incidents**

#### Epic 2 : Suivi des incidents
- **Issue 2.1 : Tableau de bord**
- **Issue 2.2 : Mise à jour des statuts**

### 1.2 Tasks pour les issues

Chaque issue est décomposée en tasks techniques. Les tâches suivantes sont accompagnées de leur code source.

---

## 2. Implémentation rapide avec code source

### **Epic 1 : Signalement des incidents**

#### **Issue 1.1 : Formulaire de signalement**

**Task 1 : Modèle Incident**

```csharp
public class Incident
{
    public int Id { get; set; }
    public string Title { get; set; }
    public string Description { get; set; }
    public string Status { get; set; } // Open, In Progress, Resolved
    public DateTime DateReported { get; set; }
}
```

**Task 2 : Migration et configuration EF Core**

- Ajoutez le contexte de base de données :

```csharp
public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) { }

    public DbSet<Incident> Incidents { get; set; }
}
```

- Ajoutez la chaîne de connexion dans `appsettings.json` :

```json
"ConnectionStrings": {
    "DefaultConnection": "Server=.;Database=IncidentTrackingDB;Trusted_Connection=True;"
}
```

- Configurez le contexte dans `Program.cs` :

```csharp
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

**Task 3 : Formulaire Razor**

- Créez une vue Razor pour signaler un incident.

```html
@model Incident

<form asp-action="Create">
    <div>
        <label for="Title">Title</label>
        <input id="Title" name="Title" type="text" required />
    </div>
    <div>
        <label for="Description">Description</label>
        <textarea id="Description" name="Description" required></textarea>
    </div>
    <button type="submit">Submit</button>
</form>
```

**Task 4 : Contrôleur Incident**

- Ajoutez une action pour afficher et traiter le formulaire.

```csharp
public class IncidentController : Controller
{
    private readonly ApplicationDbContext _context;

    public IncidentController(ApplicationDbContext context)
    {
        _context = context;
    }

    [HttpGet]
    public IActionResult Create()
    {
        return View();
    }

    [HttpPost]
    public async Task<IActionResult> Create(Incident incident)
    {
        if (ModelState.IsValid)
        {
            incident.DateReported = DateTime.Now;
            incident.Status = "Open";
            _context.Add(incident);
            await _context.SaveChangesAsync();
            return RedirectToAction("Index");
        }
        return View(incident);
    }
}
```

#### **Issue 1.2 : Validation des données**

- Ajoutez des annotations de validation dans le modèle :

```csharp
using System.ComponentModel.DataAnnotations;

public class Incident
{
    public int Id { get; set; }

    [Required]
    [StringLength(100)]
    public string Title { get; set; }

    [Required]
    [StringLength(500)]
    public string Description { get; set; }

    public string Status { get; set; }
    public DateTime DateReported { get; set; }
}
```

---

### **Epic 2 : Suivi des incidents**

#### **Issue 2.1 : Tableau de bord**

**Task 1 : Liste des incidents**

- Ajoutez une action dans `IncidentController` pour récupérer les incidents.

```csharp
public async Task<IActionResult> Index()
{
    var incidents = await _context.Incidents.ToListAsync();
    return View(incidents);
}
```

- Créez une vue Razor pour afficher la liste.

```html
@model IEnumerable<Incident>

<table>
    <thead>
        <tr>
            <th>Title</th>
            <th>Description</th>
            <th>Status</th>
            <th>Date Reported</th>
        </tr>
    </thead>
    <tbody>
        @foreach (var incident in Model)
        {
            <tr>
                <td>@incident.Title</td>
                <td>@incident.Description</td>
                <td>@incident.Status</td>
                <td>@incident.DateReported</td>
            </tr>
        }
    </tbody>
</table>
```

#### **Issue 2.2 : Mise à jour des statuts**

**Task 1 : Action de mise à jour**

- Ajoutez une méthode dans le contrôleur pour changer le statut.

```csharp
public async Task<IActionResult> UpdateStatus(int id, string status)
{
    var incident = await _context.Incidents.FindAsync(id);
    if (incident != null)
    {
        incident.Status = status;
        await _context.SaveChangesAsync();
    }
    return RedirectToAction("Index");
}
```

**Task 2 : Boutons de statut dans la vue**

- Modifiez la vue pour ajouter des boutons de changement de statut.

```html
<td>
    <a asp-action="UpdateStatus" asp-route-id="@incident.Id" asp-route-status="In Progress">In Progress</a>
    <a asp-action="UpdateStatus" asp-route-id="@incident.Id" asp-route-status="Resolved">Resolved</a>
</td>
```

---

## 3. Mise en place de la pipeline CI/CD

### 3.1 Pipeline dans Azure DevOps

Les stagiaires devront configurer eux-mêmes la pipeline CI/CD. Ils doivent inclure les étapes suivantes :

1. **Build**.
2. **Tests**.
3. **Packaging**.
4. **Déploiement** : Publication sur IIS.

