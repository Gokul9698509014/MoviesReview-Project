# MoviesReview-Project
Movies_Reviews project

#---------------urls---------------------
from django.contrib import admin
from django.urls import path
from application1 import views
urlpatterns = [
    path('admin/', admin.site.urls),
    path('',views.movieview,name=''),
    path('sample2/',views.sample1,name="sample2"),

]
#-----------------views------------------
from django.shortcuts import render
from django.http import HttpResponse
from application1.models import different

# Create your views here.


def movieview(request):
    return render(request,'first.html')

def sample1(request):
    movie=request.GET['movie']
    genra=request.GET['genra']
    date=request.GET['date']
    language=request.GET['language']
    rating=request.GET['rating']
    review=request.GET['review']

    different.objects.create(movie=movie, genra=genra, date=date, language=language, rating=rating, review=review)
    return HttpResponse(f'{movie} movie is store in db')
# ---------------models------------------
from django.db import models

# Create your models here.


class different(models.Model):
    movie=models.CharField(max_length=40)
    genra=models.CharField(max_length=40)
    date=models.DateField()
    language=models.CharField(max_length=40)
    rating=models.PositiveIntegerField()
    review=models.TextField()



# -------------------templates-----------------------

<!DOCTYPE html>

<html lang="en">
<head>
    <!-- {% load static %} -->
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- <link rel="stylesheet" href="{% static 'CSS/movie.css' %}"> -->
    <title>Document</title>
</head>
<body align="center" bgcolor="orange">

    <h1>REVIEW PAGE</h1>
    <br><br>

    <form action="{% url 'sample2' %}">
    <!-- <form action="{% url 'view' %}"> -->

        
        <label for="movie"> Movie :</label>
        <input type="text" id="movie" name="movie">
        <br><br>

        <label for="genra"> Genra: </label>
        <select name="genra" id="genra">
             <option value="action">action</option>
             <option value="advanture">advanture</option>
             <option value="comedy">comedy</option>
             <option value="horror">horror</option>
             <option value="crime">crime</option>
        </select>
        <br><br>

        <label for="date">Date: </label>
        <input type="date" id="date" name="date"> 
        <br><br>

        <label for="language">Language</label>
        <select name="language" id="language">
            <option value="Tamil">Tamil</option>
            <option value="English">English</option>
            <option value="Hindi">Hindi</option>
            <option value="Kannada">Kannada</option>
            <option value="Telugu">Telugu</option>
        </select>
        <br><br>

        <label for="rating">Rating: </label>
         
        <select name="rating" id="rating">
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
        </select>   
        <br><br>

        <label for="review">review : </label>   

        <textarea name="review" id="review" cols="30" rows="10"></textarea>  
        <br><br>

        <input type="submit" value="submit">
        <input type="reset" value="reset">
    </form>
</body>
</html>

















