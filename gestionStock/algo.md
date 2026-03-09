## Entity Categorie
type Categorie=Classe
  Debut 
     //Attributs
      public code:entier
      prive nom:chaine

      //
      prive produits:TabProduit
      prive nbre:entier
## Methodes (fonctions ou procédures)
### Constructeurs  
    public Categorie()
    Debut
    Fin
### Getters et Setters pour les attributs privés 
#### this a explique
public fonction getNom():chaine
Debut
    retourner this.nom
Fin

public procedure setNom(D nom:chaine)
Début
   si(nom!=””) alors
       this.nom←nom
   sinon
      Exception(“Le nom est obligatoire”) //Arrete le programme
   Fsi
Fin

public fonction getNbreProd():entier
Debut
    retourner this.nbre
Fin

public procedure getProduits(D/R cloneProduit:TabProduit)
var  
  i:entier
Debut
    pour(i<--1;i<=this.nbre;i<--i+1) faire
      cloneProduit[i]<--this.produits[i]
    Fpour
Fin

public fonction addProduit(D produit:Produit)
var  

Debut
   si(this.nbre<100) alors
      this.nbre<-- this.nbre+1
      this.produits[this.nbre]<--produit
     retourner Vrai
   Fsi
  retourner Faux
Fin


FinClasse
## Entity Produit
type Produit=Classe
  Debut 
     //Attributs
      prive code:entier
      prive libelle:chaine
      prive qteStock:entier
      prive prix:reel
      prive montantStock:reel //Erreur car  montantStock =prix*qteStock

      //Attributs d Navigation ==> attributs issus des relations
        //ManyToOne (+sieurs Produits ---> une categorie)
         prive categorie:Categorie
### Methodes (fonctions ou procédures)
#### Constructeurs  
public Produit()
  Debut
  Fin
#### Getters et Setters pour les attributs privés 
public fonction getLibelle():chaine
    Debut
        retourner this.libelle
    Fin
  //Setters est une procédure qui modifie la valeur de l’attribut privé
public procedure setLibelle(D libelle:chaine)
Début
   si(libelle!=””) alors
       this.libelle←libelle
   sinon
      Exception(“Le Libelle est obligatoire”) //Arrete le programme
   Fsi
Fin

public fonction getCode():entier
    Debut
        retourner this.code
    Fin
  //Setters est une procédure qui modifie la valeur de l’attribut privé
public procedure setCode(D code:entier)
Début
   si(code>0) alors
       this.code←code
   sinon
      Exception(“Le Code doit etre positif") //Arrete le programme
   Fsi
Fin

public fonction getPrix():reel
    Debut
        retourner this.prix
    Fin
  //Setters est une procédure qui modifie la valeur de l’attribut privé
public procedure setPrix(D prix:reel)
Début
   si(prix>0) alors
       this.prixk←prix
   sinon
      Exception(“Le prix doit etre positif") //Arrete le programme
   Fsi
Fin

 public fonction getQteStock():entier
    Debut
        retourner this.qteStock
    Fin
  //Setters est une procédure qui modifie la valeur de l’attribut privé
public procedure setQteStock(D qteStock:entier)
Début
   si(qteStock>0) alors
       this.qteStock←qteStock
   sinon
      Exception(“Le qteStock doit etre positif") //Arrete le programme
   Fsi
Fin

public fonction getCatgorie():Categorie
    Debut
        retourner this.categorie
    Fin
  //Setters est une procédure qui modifie la valeur de l’attribut privé
public procedure setCategorie(D categorie:Categorie)
Début
       this.categorie←categorie
Fin

#### Metiers 
public fonction calculMontant():reel
    Debut
    retourner  this.qteStock * this.prix
    Fin

 FinClasse



  
Classe Service
const N=100
type TabCategorie=tableau [1..N]Categorie
type CategorieService=Classe
type TabProduit=tableau [1..N]Produit
type CategorieService=Classe
Debut
    prive categories:TabCategorie
   prive nbreCat:entier

   public CategorieService()
   Début
     //Initialiser la valeur d’un attribut a la creation
      this.nbreCat←0
   Fin
    public fonction addCategorie(D cat:Categorie):booleen
   Début
       si(this.nbreCat<100) alors
            this.nbreCat⇐ this.nbreCat+1 
             this.categories[this.nbreCat] ← cat
            retourner Vrai
      sinon
           retourner Faux
      Fsi
   Fin

public fonction getNbreCat():entier 
Debut
   retourner this.nbreCat
Fin

public procedure getCategories(D/R cloneCategories:TabCategorie) 
  i:entier
 Debut 
     pour(i← 1;i<=this.nbreCat;i←i+1) faire
         cloneCategories[i] ←   this.categories[i]
     Fpour
  
Fin

FinClasse



type produitService=Classe
Debut
      prive produits:TabProduit
      prive nbre:entier

   public produitService()
   Début
     //Initialiser la valeur d’un attribut a la creation
      this.nbre←0
   Fin
   
    public fonction getNbreProd():entier
    Debut
        retourner this.nbre
    Fin

    public procedure getProduits(D/R cloneProduit:TabProduit)
    var  
    i:entier
    Debut
        pour(i<--1;i<=this.nbre;i<--i+1) faire
        cloneProduit[i]<--this.produits[i]
        Fpour
    Fin

    public fonction addProduit(D produit:Produit)
    var  

    Debut
    si(this.nbre<100) alors
        this.nbre<-- this.nbre+1
        this.produits[this.nbre]<--produit
        retourner Vrai
    Fsi
    retourner Faux
    Fin


FinClasse




Classe View
type CategorieView=Classe
Début
      public CategorieView()
     Début
    Fin
    public fonction saisieCategorie():Categorie
                 var 
                   categorie:Categorie
       code :entier  nom:chaine
   Début
        faire 
              Ecrire(“Entrer le code de la categorie”)
             lire(code)
        tantque(code<=0)
         faire 
              Ecrire(“Entrer le nom  de la catégorie”)
             lire(nom)
         tantque(nom=””)
         categorie←new Categorie()
         categorie.code←code
        categorie.setNom(nom)
      retourner  categorie
   Fin
  
 public procedure afficheCategories(D categories:TabCatgorie, nbre:entier)
   var 
      i:entier
Debut 
     pour(i← 1;i<=nbre;i←i+1) faire
        this.afficheUneCategorie(categories[i])
     Fpour
Fin
 prive procedure afficheUneCategorie(D cat:Categorie)
Debut 
           Ecrire(“Code :”, cat.code,” Nom: ” ,cat.getNom())
Fin


FinClasse


















Classe Principal
Type Principal =Classe
Debut
    public Principal()
    Debut
    Fin
  public  procedure main()
   var
     //Déclaration
      catView: CategorieView
      catService:CategorieService
      cat : Categorie  result:booleen
     cloneCategories:TabCategorie
  Début
      catView←new CategorieView()
        catService←new catService()
       //1-Menu 
      //2-Saisie du choix 
      Cas Vaut (choix)
        1:  //Creer une Categorie
         cat ← catView.saisieCategorie()
          result←  catService.addCategorie(cat)
          si(result =Vrai) alors 
            Ecrire (“Catégorie ajoutée avec succès”)
         sinon 
                Ecrire (“Le Tableau est rempli”)
        Fsi
         2:  //Lister les  Catégories
          catService.getCategories(cloneCategories)
           catView.afficheCategories(cloneCategories,catService.getNbreCat())
 Fin
FinClasse
