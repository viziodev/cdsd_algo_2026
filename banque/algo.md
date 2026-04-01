# Entity
type Client=Classe
Debut
  prive nom:chaine
  prive prenom:chaine
  prive tel:chaine
  prive login:chaine
  prive password:chaine

  //Proprites de  Navigation
  prive compte:Compte

  public Client()
  Debut
  Fin
 //Surchage
  public Client(D nom,prenom,tel,login,password:chaine,compte:Compte)
  Debut
       this.nom<--nom
       this.prenom<--prenom
       this.tel<--tel
       this.login<--login
       this.password<--password
        this.compte<--compte
  Fin
  1. Getters et Setters
    //nom,prenom,tel,login,password


public fonction recuperCompteUnClient():Compte
Debut
     retourner this.compte
Fin

public procedure attribuerUnCompte(D compte:Compte)
Debut
      this.compte<--compte
Fin

FinClasse

type Compte=Classe
Debut
prive solde:reel
public Compte()
Debut
Fin

public Compte(D solde:reel)
Debut
    this.solde<--solde
Fin

public fonction consulterSolde():reel
Debut
   retourner this.solde
Fin

Fin

# Service
const N=100
type TabClient=tableau[1..N]Client
type ClientService=Classe
Debut
  prive static  clients:TabClient
  prive static  nbreClient:entier

prive ClientService()
Debut
Fin


//Fixtures ==>Fausses Donnees
public static procedure initialize()
var 
  i:entier
Debut
      pour(i<--1;i<=5;i<--i+1) faire 
           this.clients[i]<--new Client("Client"+i,
           "Client"+i,"77100101"+i,"client"+i,"client"+i,
            new Compte(10000*i)
           )
      Fpour

Fin

public static fonction seConnecter(D login,password:chaine):Client|null
var 
  i:entier
Debut
     pour(i<--1;i<=this.nbreClient;i<--i+1) faire
        Si(this.clients[i].getLogin()==login et this.clients[i].getPassword()==password) alors
         retourner this.clients[i]
        Fsi
     Fpour
     retourner null
Fin

FinClasse

# View
type ClientView=Classe
Debut
    prive ClientView()
    Debut
    Fin
     public static procedure menu(D client:Client)
     var 
       choix:entier
       compte:Compte
     Debut
       compte<--client.recuperCompteUnClient()
      faire 
        Ecrire("1-Consulter Solde")
        Ecrire("2-Voir Historique Transaction")
        Ecrire("3-Faire un Virement")
        Ecrire("4-Quitter")
        lire(choix)
        cas(choix) vaut
         1: 
             Ecrire ("Le Solde du Compte est ",compte.consulterSolde())

       FinCas

      tanque()
     Fin
FinClasse


type App=Classe
Debut
    prive App()
    Debut
    Fin
     public static procedure main()
     var 
        result:Client
        login,password:chaine
     Debut 
         ClientService.initialize()
        faire
           faire
               Ecrire("Entrer le Login")
               lire(login)
           tantque(login="")

           faire
               Ecrire("Entrer le Password")
               lire(password)
           tantque(password="")
            result<-- ClientService.seConnecter(login,password)
           si(resut=null) alors
             Ecrire("Login ou Mot de passe Incorect")
           Fsi
          tantque(result=null)
         ClientView.menu(resut)
         
     Fin
FinClasse

