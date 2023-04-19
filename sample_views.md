Example View for Displaying Animals by Weather Code:

- Front End passes weather code (3-digit number) for current forecast into the URL in their GET request

```python
from rest_framework import generics
from is_it_raining.models import Animal
from is_it_raining.serializers import AnimalSerializer

class AnimalByWeatherCodeView(generics.RetrieveAPIView):
    serializer_class = AnimalSerializer
    
    def get_object(self):
        weather_code = self.kwargs['weather_code']
        animal = Animal.objects.filter(weather__weather_code=weather_code).first()
        return animal
 ```
 
 - The .first() returns the first animal object in the list that has the matching weather code. If none is found, 'first' returns None.
 - If we need to, maybe later we can have a set of animals for each weather code and return a random animal from that set...
