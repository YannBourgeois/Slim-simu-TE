# Slim-simu-TE
A short SLIM script to simulate an Arabidopsis TE insertion

To execute over the parameters in the paper:
sel_TE is the selective advantage s of the TE during drought
del_sel_TE is the selective disadvantage of the TE during normal conditions
n_drought_event controls the number of drought events (in generations). These events are placed at regular intervals. For example, if it is set to 4 and each drought lasts two generations,
the droughts start at generation 1, 17, 34 and 49.
drought_length controls the length (in generations) of each drought event.

for sel_TE in 0.5 1 2 5
do
for del_sel_TE in 0.1 0.2 0.5 0.9
do
for n_drought_event in 1 2 3 4
do
for drought_length in 2 3 4
do
for i in {1..1000}
do
slim -d sel_TE=$sel_TE -d del_sel_TE=$del_sel_TE -d n_drought_event=$n_drought_event -d drought_length=$drought_length script.slim | grep Ad | cut -f1,2,5,7,10,13 -d " " | sed "s:Advantage_TE:$n_drought_event $drought_length $i:" >> results.txt
done
done
done
done
done


