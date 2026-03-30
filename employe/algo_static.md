# Menu
   1-Ajouter un Employe
   2-Affecter un Employe a un Departement
   3-Afficher les  Employe d'un Departement
   4-Afficher Tous les  Employes 
   5-Quitter

  

# Entity
type Departement=Classe
Debut 
  prive code : entier
  prive nom : chaine
  prive employes:TabEmploye
  prive nbreEmploye:entier

  public Departement()
  Debut
     this.nbreEmploye<-0
  Fin
 public Departement(D code : entier,  nom : chaine)
  Debut
     this.code<=code
     this.nom<=nom
     this.nbreEmploye<-0
  Fin

  //Getters et Setters

  //ToChaine
  public fonction toChaine():chaine
  Debut
    retourner "Code ",this.code," Nom :",this.nom
  Fin

public fonction getNbreEmploye():entier
Debut
   retourner this.nbreEmploye
Fin

public fonction addEmploye(D employe:Employe):booleen
Debut
   si(this.nbreEmploye<N) alors
       this.nbreEmploye <- this.nbreEmploye+1
       this.employes[this.nbreEmploye]<--employe
       retourner Vrai
   Fsi
   retourner Faux
Fin

public procedure getEmployes(D/R allEmployes:TabEmploye)
var
 i:entier
Debut
   pour(i<--1;i<=this.nbreEmploye;i<--i+1) faire
     allEmployes[i]<-- this.employes[i]
   Fpour
Fin


FinClasse

type Employe=Classe
Debut 
  prive matricule : chaine
  prive nom : chaine

  prive departement:Departement

  public Employe()
  Debut
  Fin
 public Employe(D matricule : chaine,  nom : chaine)
  Debut
     this.matricule<=matricule
     this.nom<=nom
  Fin

  //Getters et Setters

  //ToChaine
  public fonction toChaine():chaine
  Debut
    retourner "Matricule ",this.matricule," Nom :",this.nom
  Fin
  public fontion getDepartement():Departement
  Debut
    retourner this.departement
  Fin

  public procedure affecterDepartement(D departement:Departement)
  
  Debut
     this.departement<--departement
  Fin

    
FinClasse
const N=100
Type TabEmploye =tableau [1..N]Employe
Type TabDepartement =tableau [1..N]Departement

# Services

type static EmployeService=Classe
Debut
    prive static employes:TabEmploye
    prive static nbreEmploye:entier
    prive EmployeService()
    Debut
    Fin

    public static fonction getNbreEmploye():entier
    Debut
    retourner this.nbreEmploye
    Fin

public static fonction addEmploye(D employe:Employe):booleen
Debut
   si(this.nbreEmploye<N) alors
       this.nbreEmploye <- this.nbreEmploye+1
       this.employes[this.nbreEmploye]<--employe
       retourner Vrai
   Fsi
   retourner Faux
Fin

public static procedure getEmployes(D/R allEmployes:TabEmploye)
var
 i:entier
Debut
   pour(i<--1;i<=this.nbreEmploye;i<--i+1) faire
     allEmployes[i]<-- this.employes[i]
   Fpour
Fin

public static fonction  getEmployeByMatricule(D matricule:chaine): Employe|null

    i:entier
Debut
   pour(i<--1;i<=this.nbreEmploye;i<--i+1) faire
     si(this.employes[i].getMatricule()==matricule) alors
        retourner this.employes[i]
     Fsi
   Fpour
     retourner null
Fin

type static DepartementService=Classe
Debut
    prive static departements:TabDepartement
    prive static nbreDepartement:entier
    prive DepartementService()
    Debut
    Fin

    public static fonction getNbreDepartement():entier
    Debut
    retourner this.nbreDepartement
    Fin



public static procedure getDepartements(D/R allDepartement:TabDepartement)
var
 i:entier
Debut
   pour(i<--1;i<=this.nbreDepartement;i<--i+1) faire
     allDepartement[i]<-- this.departements[i]
   Fpour
Fin

public static fonction  updateEmploye(D  employeWithDept:Employe):booleen
    
 i:entier
Debut
   pour(i<--1;i<=this.nbreEmploye;i<--i+1) faire
     si(this.employes[i].getMatricule()=employeWithDept.getMatricule()) alors
        this.employes[i]<--employeWithDept
        retourner Vrai
     Fsi
   Fpour
     retourner Faux

FinClase


# Views

type static EmployeView=Classe
Debut
 public EmployeView()
 Debut
 Fin

 public static fonction saisieEmploye():Employe
 var
   emp:Employe
   matricule,nom:chaine
 Debut
    faire
    Ecrire("Entrer le Matricule")
    lire(matricule)
    tantque(matricule="")

    faire
    Ecrire("Entrer le Nom")
    lire(nom)
    tantque(nom="")
    //Le  Departement a null que l'employe n'a pas de departement
    emp.setDepartement(null)
    emp<--new Employe(matricule,nom)
    retourner  emp
 Fin

public static procedure afficheEmployes( D employes:TabEmploye,nbreEmploye:entier)
 var 
  i:entier
 Debut
    pour(i<--1;i<=nbreEmploye;i<--i+1) faire
       Ecrire(employes[i].toChaine())
   Fpour
 Fin

 public static fonction selectionnerDepartement( D departements:TabDepartement,nbreDepart:entier):Departement
 var 
  i:entier
  indexDepart:entier
 Debut
    pour(i<--1;i<=nbreDepart;i<--i+1) faire
       Ecrire(i,"-",departements[i].getNom())
       faire
         lire(indexDepart)
       tanque(indexDepart<0 || indexDepart>nbreDepart)
    Fpour
    retourner departements[indexDepart];

 Fin


FinClasse

# Principal
type static App=Classe
Debut
 prive App()
 Debut
 Fin

 public static procedure main()
  var 
    choix:entier
    emp,empSerch:Employe
    result:booleen
    allEmployes:TabEmploye nbreEmp:entier
    rep:Caractere
    allDepartements:TabDepartement,nbreDepart:entier
    dept:Departement
    nbreEmpDept:entier
    allEmployesByDept:TabEmploye 
    matricule:chaine
 Debut
 
   faire
     Ecrire("1-Ajouter un Employe")
     Ecrire("2-Afficher les  Employes d'un departement")
     Ecrire("3-Afficher les  Employe tous les employes")
     Ecrire("4-Affecter un employe a un departement")
     Ecrire("5-Quitter")
     lire(choix)

     cas (choix) vaut
        1: 
             emp<--empView.saisieEmploye()
             Ecrire("Voulez vous Affecter un Departement a cette employe(O/N)")
             lire(rep)
             si(rep='O') alors
                   DepartementService.getDepartements(allDepartements)
                   nbreDepart<--DepartementService.getNbreDepartement()
                   dept<--EmployeView.selectionnerDepartement(allDepartements,nbreDepart)
                   //Relation  ManyToOne (Employe-->Departement)
                        emp.affecterDepartement(dept)
                   //Relation  OneToMany (Departement--->Employe)
                     dept.addEmploye(emp)
             Fsi
               result<-- EmployeService.addEmploye(emp)
            si(result=Vrai) alors
              Ecrire("Employe ajouter avec success")
            sinon
              Ecrire("Le Tableau est rempli")
            Fsi

        2: 
             dept<--EmployeView.selectionnerDepartement(allDepartements,nbreDepart)
             nbreEmpDept<--dept.getNbreEmploye()
             dept.getEmployes(allEmployesByDept)
             EmployeView.afficheEmployes(allEmployesByDept,nbreEmpDept)

        3: 
          EmployeService.getEmployes(allEmployes)
          nbreEmp<--EmployeService.getNbreEmploye()
          EmployeView.afficheEmployes(allEmployes,nbreEmp)
     
        4: 
          empSerch<--null
        faire
             Ecrire("Entrer le matricule de l'employe Recherche")
             lire(matricule)
             si(matricule!="") alors
                empSerch<--EmployeService.getEmployeByMatricule(matricule)
             FinSi
         tanque(empSerch=null)
         si(empSerch.getDepartement()!=null)  alors
            Ecrire ("Cette Employe a deja un departement")
         sinon
             dept<--EmployeView.selectionnerDepartement(allDepartements,nbreDepart)
             //Relation  ManyToOne (Employe-->Departement)
               emp.affecterDepartement(dept)
             //Relation  OneToMany (Departement--->Employe)
              dept.addEmploye(emp)

              //Modifier employe dans le service
               result<-- EmployeService.updateEmploye(emp)

              si(result=Vrai) alors
                 Ecrire("Affectation reussie")
            sinon
                  Ecrire("Erreur Affectation")
            Fsi
         Fisi

         


     FinCas 
   tantque(choix!=5)

 Fin

 
FinClasse