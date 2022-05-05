# Cors Para GoLang 
## Solução do erro de Cors GoLang com Front End react JS
#### Access to XMLHttpRequest at 'http://localhost:5000' from origin 'http://localhost:3000' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource.

```

package main

import (
	"fmt"
	"log"
	"net/http"

	"github.com/gorilla/mux"
	"github.com/rs/cors"
)

func main() {
	r := mux.NewRouter()
	PORT := 5000

	r.HandleFunc("/", func(rw http.ResponseWriter, r *http.Request) {
		rw.WriteHeader(http.StatusOK)
		_, err := rw.Write([]byte("Hello World!"))
		if err != nil {
			log.Fatal(err)
		}
	}).Methods(http.MethodGet)

	corsHandler := cors.New(cors.Options{
		AllowedOrigins: []string{"http://localhost:3000"},
		AllowedHeaders: []string{"*"},
	}).Handler(r)

	fmt.Printf("Server on Port: %d", PORT)
	log.Fatal(http.ListenAndServe(fmt.Sprintf(":%d", PORT), corsHandler))
}


```
