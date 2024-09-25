# Optimizing-parks-for-neighborhoods

/*********************************************
 * OPL 12.6.0.0 Model
 * My own model
 *********************************************/

int k=...; // Number of known parks
int n =...; //Number of new parks is n
range park = 1..k+n;
range newpark= k+1..k+n;
int l =...; //Numbers of neighborhoods
range neighborhood = 1..l;


/*PARAMETERS*/
float C =...; //cost for new park
float B =...; //budget
float A =...; // profit 
float DMAX=...; // max distance
float D[neighborhood][park]=...; //distance form park to neighborhood
int P[neighborhood]=...; //citizens in neighborhood

/*VARIABLRS*/
dvar boolean Y[newpark]; // Y[j] = 0 no new park, Y[j]=1 new park
dvar boolean X[neighborhood][park]; // X[ij] = 0 park i  NO belong to neighborhood j ,X[ij] park i belong to neighborhood j 


/* objective */
maximize 
sum(j in neighborhood, i in park)A*P[j]*X[i][j] - sum(j in newpark)Y[j]*C;

/* Contraints */
subject to 
{
forall (i in neighborhood) sum(j in park)X[i][j] <= 1;

forall (i in park) sum (j in neighborhood)X[i][j] <= k+n;

forall (i in neighborhood , j in park)X[i][j]* D[i][j] <= DMAX;

forall (i in neighborhood) sum(j in newpark)C*Y[j] <= B;


forall (i in  neighborhood ,j in newpark)X[i][j] <= Y[j];








}
