---
type: post
layout: default
title: Evolving strings with Genetica
summary: A small example on how to use the Genetica Ruby gem.
language: english
comments: true
---

> *Warning:* this is an easy example on how to use *Genetica* (the Ruby gem) to create genetic algorithms; anyway you will need some basic knowledge about genetic algorithms to understand it. Maybe you should read [something][wikipedia_ga] about the subject before start to read this post.

One of the most common and simple examples on how to use genetic algorithms to solve problems is the evolution of strings. Usually an initial string is provided to the algorithm, then the algorithm will try to evolve a random string (or a population of strings) until it matches the initial one, using a string distance algorithm as the fitness function.

In this example we will use the [*Genetica*](https://rubygems.org/gems/genetica) Ruby gem. The actual version of the gem is *0.0.1.beta.2*, this is the version that we will use to run this example. You can use the following command to install it:

{% highlight bash %}
$ gem install genetica --pre
{% endhighlight %}

After install it you can use the Ruby *require* statement to load the gem in your scripts:

{% highlight ruby %}
require 'genetica'
{% endhighlight %}

## Defining the fitness function

Define a correct fitness function is one of the most important steps in the creation of a genetic algorithm. The fitness function will measure the distance between the solution that a chromosome of the population represents and the expected solution that we try to get. In our case we want to get a initial string so we will try to measure the distance between the initial string and the represented by the chromosome.

In *Genetica* a fitness function always must receive an unique parameter (a chromosome) and will return a value that represent the fitness of this chromosome.

In this example we will generate chromosomes with a length equal to the length of the initial string so we only need to calculate the number of characters in the chromosome that match with the characters in the initial string. This word distance will be the fitness value for every chromosome in the population. If, for example we define an initial string "Genetics" and a chromosome represents the string "Genetiza" we will get a fitness of 6 (six characters match).

We will define our fitness function as follows:

{% highlight ruby %}
WORD = "Genetics"

def word_distance(chromosome)
  (0...WORD.size).inject(0) do |distance, index|
    if WORD[index] == chromosome.chromosome[index]
      distance += 1
    else
      distance
    end
  end
end
{% endhighlight %}

## Setting the chromosome population

To obtain good results using genetic algorithms it is important to choose a convenient set of parameters for the chromosome population.

Set all the parameters of a population is very easy using *Genetica*, you must only to create a *PopulationBuilder*, a class that will build custom chromosome populations for us in a convenient way:

{% highlight ruby %}
population_builder = Genetica::PopulationBuilder.new
{% endhighlight %}

Once you have created a *PopulationBuilder* is very easy to start customizing the population that will be created. Next we will see all the different parameters that can be modified for a *PopulationBuilder*.

### Size

Size refers to the number of chromosomes that will live in a population. In this example we will set a number of 100 chromosomes for every population. We can set this parameter with the following statement:

{% highlight ruby %}
population_builder.size = 100
{% endhighlight %}

*PopulationBuilder* has a default values for all population parameters. In this case the default value for *size* is 20. You can see all the default values defined [here](https://github.com/jfcalvo/Genetica/blob/master/lib/genetica/population_builder.rb#L15).

### Elitism

When you use a value greater than 0 for the elitism parameter a group of the best chromosomes of the population (chromosomes with the best fitness) will be forced to be saved, moving to the next generation. This technique attempts to ensure that a group of the best chromosomes (the elite) will be in the next generation, improving the quality of the population. If you set this parameter with a value of 0 the elitism is disabled for the population. In this example we have chosen a *elitism* of 5.

{% highlight ruby %}
population_builder.elitism = 5
{% endhighlight %}

By default *PopulationBuilder* disables *elitism* so this parameter has a default value of 0.

### Crossover probability

[Crossover][wikipedia_crossover] probability defines how often will be chromosome crossover performed. With *Genetica* this parameter is defined with a value between 0.0 and 1.0, with 0.0 deactivating crossover and 1.0 as a 100% possibility of crossover. In this example we will set a crossover probability of 70% (with a value of 0.7).

{% highlight ruby %}
population_builder.crossover_probability = 0.7
{% endhighlight %}

*PopulationBuilder* set a default value of 0.7 for *crossover probability*.

### Mutation probability

[Mutation][wikipedia_mutation] probability defines how often the chromosome [alleles](http://en.wikipedia.org/wiki/Alleles) will be mutated for every chromosome in the population. Similarly to crossover probability, mutation probability uses a values between 0.0 and 1.0 to define the probability of mutation. We will set a probability of 0.1% (a value of 0.01).

{% highlight ruby %}
population_builder.mutation_probability = 0.01
{% endhighlight %}

*Mutation probability* is initialized with a value of 0.001 (0.1%) by *PopulationBuilder* class.

### Chromosome length

The chromosome length defines the number of alleles that the chromosome will have. In this example we try to evolve chromosomes to match an initial string so the chromosome length in this case will be the length of the initial string. (e.g 8 if we use the initial string "Genetics").

{% highlight ruby %}
population_builder.chromosome_length = 8
{% endhighlight %}

*Chromosome length* have a value of 8 by default defined by *PopulationBuilder*.

### Chromosome alleles

This parameter defines the different values that a chromosome [allele](http://en.wikipedia.org/wiki/Allele) can have. Because we are evolving strings is logical that we use the set of all usable characters. We define this parameter with the following line:

{% highlight ruby %}
population_builder.chromosome_alleles = ('a'..'z').to_a + ('A'..'Z').to_a + [' ']
{% endhighlight %}

Alleles of a population are defined as arrays in Genetica, by default *PopulationBuilder* sets a default value of `[0, 1]` (binary values) for the alleles of a population.

### Fitness function

Since our fitness function is an ordinary Ruby function we need to reference this function with the following syntax:

{% highlight ruby %}
population_builder.fitness_function = method(:word_distance)
{% endhighlight %}

*Fitness function* has not default value so you are forced to define one. Errors will occur if the population is run without a defined *fitness function*.

### Building the population

To finally build the population we can use the next line:

{% highlight ruby %}
population = population_builder.population
{% endhighlight %}

## Living and dead. Running generations

Once we have finally created our population we need to start the generation cycle and run the population. We will create a while loop that will test if some chromosome has a fitness of 8 (the best possible fitness) because the initial string that we are using is "Genetics" (with a length of 8). If population comes to have a best fitness of 8 that means that a chromosome in the population has reached the solution and we have finished the execution of the program:

{% highlight ruby %}
while population.best_fitness < 8
  population.run generations=1
end
{% endhighlight %}

## Some runs

The final script is more complex that the example code show here, it can receive a string as parameter and will try to evolve the population until the initial string is found. Here we can see some sample executions with different strings:

{% highlight bash %}
$ ./word.rb Genetics
GhCntJJz, generation: 1, distance: 2
GCOrYiGs, generation: 2, distance: 3
GCOrYiGs, generation: 3, distance: 3
GwnehZSs, generation: 4, distance: 4
OerItics, generation: 5, distance: 5
OerItics, generation: 6, distance: 5
GerItics, generation: 7, distance: 6
GerItics, generation: 8, distance: 6
GerItics, generation: 9, distance: 6
GerItics, generation: 10, distance: 6
GerItics, generation: 11, distance: 6
GenItics, generation: 12, distance: 7
GenItics, generation: 13, distance: 7
GenItics, generation: 14, distance: 7
GenItics, generation: 15, distance: 7
GenItics, generation: 16, distance: 7
Genetics, generation: 17, distance: 8
Solution at generation: 17.
{% endhighlight %}

{% highlight bash %}
$ ./word.rb 'Hello World!'
HMWlWXWsHndR, generation: 1, distance: 4
HKylj UDEldK, generation: 2, distance: 5
HKylj UDEldK, generation: 3, distance: 5
HMWloIHorltE, generation: 4, distance: 6
HMWloIHorltE, generation: 5, distance: 6
HKylU WPrldY, generation: 6, distance: 7
HKylU WPrldY, generation: 7, distance: 7
HeElj jorll!, generation: 8, distance: 8
HeElo WoDld , generation: 9, distance: 9
HeElo WoDld , generation: 10, distance: 9
HeElo WoDld!, generation: 11, distance: 10
HeElo WoDld!, generation: 12, distance: 10
HeElo WoDld!, generation: 13, distance: 10
Hfllo World!, generation: 14, distance: 11
Hfllo World!, generation: 15, distance: 11
Hfllo World!, generation: 16, distance: 11
Hfllo World!, generation: 17, distance: 11
Hello World!, generation: 18, distance: 12
Solution at generation: 18.
{% endhighlight %}

## Source code

You can see the complete source code of this example [here](https://github.com/jfcalvo/Genetica/blob/master/examples/word.rb).

[wikipedia_ga]: http://en.wikipedia.org/wiki/Genetic_algorithm
[wikipedia_crossover]: http://en.wikipedia.org/wiki/Crossover_(genetic_algorithm)
[wikipedia_mutation]: http://en.wikipedia.org/wiki/Mutation_(genetic_algorithm)
