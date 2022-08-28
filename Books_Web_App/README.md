## Flask and Jinja Web Server

Add Bootstrap Navigation and image upload
New routes addbook, addimage

# How to execute this project
1. Open a terminal window and instal `flask-restful` and `flas-jwt-extended` libraries using the following commands: 
```
pip install flask-restful
```
```
pip install flask-jwt-extended
```
2. All templates and code required are contained within this repo folder
3. Books are defined in the app.py file as a list of dictionaries
4. Book images are stored in the static folder and referenced in the book.html with the following format `<img src="static/image{*book_id_reference*}.png" width = "50">`
5. Users are identified in the app.py file in a list of dictionaries
6. Run the app.py in VS Code in the run/debug mode.  
7. Confirm functionality: Add books via the 'Add Book' route. Try this with both admin and non-admin login's to confirm authorization restrictions for adding books. 
