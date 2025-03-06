% База фактов (динамическая)
:- dynamic preference/1.

% Продукционные правила с русскоязычными фильмами
recommend('1+1') :- 
    preference(комедии), 
    preference(настроение_весёлое).

recommend('Побег из Шоушенка') :- 
    preference(драмы), 
    preference(настроение_задумчивое).

recommend('Джон Уик') :- 
    preference(боевики), 
    preference(короткий_фильм).

recommend('Интерстеллар') :- 
    preference(фантастику), 
    preference(длинный_фильм).

recommend('Один дома') :- 
    preference(комедии), 
    preference(известные_актёры).

recommend('Достучаться до небес') :- 
    preference(драмы), 
    preference(короткий_фильм).

recommend('Дэдпул') :- 
    preference(боевики), 
    preference(настроение_весёлое).

recommend('Начало') :- 
    preference(фантастику), 
    preference(настроение_задумчивое).

recommend('Зверополис') :- 
    preference(короткий_фильм), 
    preference(настроение_весёлое).

recommend('Зелёная миля') :- 
    preference(длинный_фильм), 
    preference(драмы).

% Очистка предпочтений перед новым запросом
clear_preferences :- retractall(preference(_)).

% Добавление предпочтения
add_preference(P) :- assertz(preference(P)).

% Главная процедура рекомендации с русскоязычным выводом
run_recommendation :-
    findall(Movie, recommend(Movie), Movies),
    list_to_set(Movies, UniqueMovies),
    (   UniqueMovies \= []
    ->  write('Рекомендуемые фильмы: '), nl, 
        print_movies(UniqueMovies)
    ;   write('Фильм не найден.'), nl
    ).

print_movies([]).
print_movies([H|T]) :- 
    write(H), nl, 
    print_movies(T).
