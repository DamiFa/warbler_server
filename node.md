# JWT
Est un token contenant des infos sur l'user. Il est protégé par un "secret".

Le front end le passe dans le header.authorization

# BCRYPT
Permet d'encrypter un mdp. On encrypte le mdp avant de le mettre dans la base de donnée. 

(avec mongoose:)
```
userSchema.pre("save", async function(next){
  try{
    if(!this.isModified('password')){
      return next();
    }
    let hashedPassword = await bcrypt.hash(this.password, 10);
    this.password = hashedPassword;
    return next();
  } 
  catch(err){
    return next(err);
  }
});
```

On passe ensuite à notre Schema Mongoose une methode qui permettra de comparer le mdp stocké avec un passé par l'user:
```
userSchema.method.comparePassword = async function(candidatePassword, next){
  try {
    let isMatch = await bcrypt.compare(candidatePassword, this.password);
    return isMatch;
  } catch (err) {
    return next(err);
  }
};
```

# DOTENV
Package qui permet de définir des variables d'environenment

# DEVELOPEMENT D'UN PROJET

## ORGANISATION DE L'ESPACE DE TRAVAIL

