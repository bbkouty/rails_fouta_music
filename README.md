# 🎵 Rails Project – Albums & Tracks

## 📌 Description

Ce projet est une application Ruby on Rails permettant de gérer une base de données musicale composée de Albums et Tracks.
Il s’agit d’un exercice pratique pour se familiariser avec :
- La création de models et leurs migrations
- L’utilisation de seeds.rb pour peupler la base
- Les requêtes ActiveRecord dans la console Rails (rails console)

## ⚙️ Installation

1. Clone ce dépôt (ou crée ton projet) :
```
git clone <url-du-repo>
cd rails_fouta_music
```
2. Installe les dépendances :
```
bundle install
```

## 🗄️ Base de données

Crée la base de données et applique les migrations :
```
rails db:create db:migrate
```
Peuple la base avec les données de test :
```
rails db:seed
```

## 📂 Models

Album
- title (string) : titre de l’album
- artist (string) : nom de l’artiste

Track
- title (string) : titre de la chanson
- album (string) : titre de l’album
- artist (string) : artiste
- duration (integer) : durée (ms)
- size (integer) : taille (octets)
- price (float) : prix

## 🧑‍💻 Utilisation

Lance la console Rails :
```
rails console
```

## 📚 Exercices

Réponses aux questions : 

#### a) Niveau facile

```
# Nombre total d'albums
Album.count  

# Auteur de la chanson "White Room"
Track.find_by(title: "White Room").artist  

# Chanson qui dure 188133 ms
Track.find_by(duration: 188133).title  

# Groupe de l’album "Use Your Illusion II"
Album.find_by(title: "Use Your Illusion II").artist
```

#### b) 

```
# Albums contenant "Great"
Album.where("title LIKE ?", "%Great%").count  

# Supprimer albums contenant "music"
Album.where("title LIKE ?", "%music%").destroy_all  

# Albums de AC/DC
Album.where(artist: "AC/DC").count  

# Chansons durant 158589 ms
Track.where(duration: 158589).count
```

#### c) Niveau difficile (boucles en console)

```
# Tous les titres de AC/DC
Track.where(artist: "AC/DC").each { |t| puts t.title }

# Tous les titres de l'album "Let There Be Rock"
Track.where(album: "Let There Be Rock").each { |t| puts t.title }

# Prix + durée totale de l'album "Let There Be Rock"
tracks = Track.where(album: "Let There Be Rock")
total_price = tracks.sum(:price)
total_duration = tracks.sum(:duration)

puts "Prix total: #{total_price}, Durée totale: #{total_duration} ms"

# Coût total discographie de Deep Purple
deep_purple_tracks = Track.where(artist: "Deep Purple")
puts "Prix discographie Deep Purple: #{deep_purple_tracks.sum(:price)}"

# Modifier tous les titres de "Eric Clapton" → "Britney Spears"
Track.where(artist: "Eric Clapton").each do |track|
  track.update(artist: "Britney Spears")
end
```

## 📝 Notes

- Tu peux réinitialiser la BDD à tout moment avec :
```
rails db:drop db:create db:migrate db:seed
```
---