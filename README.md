package main
 import (
	"fmt"
	"log"
	"net/http"
"math/rand"
 "strconv"
          
 )

 type Movie struct{
	ID string  "json:ID"
	Title string "json:Title"
	Ibsn int "json:Year"
	Director *director "json:Director"

 }

 type Director struct{
	Firstname string "json:Firstname"
	Lastname string "json:Lastname"
 }

 var Movie []Movie

 func getMovies(w http.ResponseWriter, r *http.Request) {
	 w.Header().Set("Content-Type", "application/json")
	 json.NewEncoder(w).Encode(Movie)
 }


 func deleteMovie(w http.ResponseWriter, r *http.Request) {
	 w.Header().Set("Content-Type", "application/json")
	 params := mux.Vars(r)
	 for index, item := range Movie {

		 if item.ID == params["id"] {
			 Movie = append(Movie[:index], Movie[index+1:]...)
			 break
		 }
	 }
	 json.NewEncoder(w).Encode(Movie)

 }

 func getMoviesByDirector(w http.ResponseWriter, r *http.Request) {
	 w.Header().Set("Content-Type", "application/json")
	 params := mux.Vars(r)
	 for _, item := range Movie {
		 
		 if item.Director == params["director"] {
			 json.NewEncoder(w).Encode(item)
			 
		 }

	func updateMovie()  { w.http ResponseWriter, r *http.Request) {
		w.Header().Set("Content-Type", "application/json")
	}
		w.Header().Set("Content-Type", "application/json")
		params := mux.Vars(r)
		for index, item := range Movie {
			if item.ID == params["id"] {
				Movie = append(Movie[:index], Movie[index+1:]...)
				var movie Movie
				_ = json.NewDecoder(r.Body).Decode(&movie)
				movie.ID = params["id"]
				Movie = append(Movie, movie)
				json.NewEncoder(w).Encode(movie)
                 return
				
			}
		}


		
	}
	 }
 }
 func main () {
	 r := mux.NewRouter()
	 movies := []Movie{
		 {ID: "1", Title: "The Dark Knight", Year: 2008, Director: &Director{Firstname: "Christopher", Lastname: "Nolan"}},
		 {ID: "2", Title: "The Avengers", Year: 2012, Director: &Director{Firstname: "Joss", Lastname: "Whedon"}},
		 r.HandlerFunc("/movies", getMovies).Methods("GET")
		 r.HandlerFunc("/movies/{id}", getMovie).Methods("GET")
		 r.HandlerFunc("/movies", createMovie).Methods("POST")
		 r.HandlerFunc("/movies/{id}", updateMovie).Methods("PUT")
		 r.HandlerFunc("/movies/{id}", deleteMovie).Methods("DELETE")
		 r.HandlerFunc("/movies/director/{director}", getMoviesByDirector).Methods("GET")
		 fmt.Printf("Starting server at port 8080\n")
		 log.Fatal(http.ListenAndServe(":8080", r))
	 }
 }
