# Improved Genetic Algorithm for Optimizing Microgrid Scheduling (Considering Environmental Factors)

​  
Microgrid control is complex. Improved genetic algorithms are used to create island microgrid models and optimize system generation. The model will be tested by simulating the control of this microgrid model within 24 hours.
2. Result Display
Run Result:
Editor
Editor
Editor
Editor
2.2 Situation Two - Editor
Editor
Editor
Editor
Editor
2.3 Situation Three - Editor
Editor
Editor
Editor
Editor
2.4 Situation Four   Editor
This will take longer to run, so I'm not waiting for it to finish; I'll just go ahead and show you the code.
3. Matlab code implementation (with code data, also need documentation explanation) Here only display the main function part of the code, all code can be found in:
Editor
\n%% MATLB|Improved Genetic Algorithm Optimization for Microgrid Scheduling (Considering the Environment)\n\nclear\nclc\nclose all\n\n\npop=100;            % Population size\nm_rate = .1;        % Mutation rate\nc_pt = 2;           % Intersection point\ngood_enough = .08;  % When to stop\nweights = [1, .6, .4];\n%% Chromosome\npower = 1;\ncost = 2; \nemission = 3;\nsource_1 = [20, .02, .01];\nsource_2 = [120, .20, .05];\nsource_3 = [15, .01, .02];\nsource_4 = [50, .02, .04];\nsources = [source_1; source_2; source_3; source_4];\n\n%===== Define Range ==========================\n[num_sources, num_genes] = size(sources);\nboundaries = zeros(num_genes, 2);\nboundaries(1,:) = [15, 100];        %Power Range\nboundaries(2,:) = [.15, 6.55];      % The lowest cost to achieve maximum power\nboundaries(3,:) = [.15, 3.75];      % The minimum emission with maximum power\n\n\n\n%% Selection strategy\ndisp('Choose a Reproduction Method');\nr = input(' 1 - Mutation\n 2 - Crossover\n ');\nwhile r > 2 || r < 1\n    r = input(' \nInput a valid number\n 1 - Mutation\n 2 - Crossover\n ');\nend\ndisp('' );\ndisp('Choose a Survival Method');\ns = input('1 - Random Selection\n 2 - Elitism\n ');\nwhile s > 2 || s < 1\n    s = input(' \nInput a valid number\n 1 - Random Selection \n 2 - Elitism\n ');\nend\ndisp('');\n\n\nif r == 1\n    reproduction = @mass_mutate;\nelse\n    reproduction = @crossover;\nend\n\nif s == 1\n    survival = @random_selection;\nelse\n    survival = @elitism;\nend\n\n%% Load sequence\nload = TimeSeries();\n\n%% Generate initial generation\nchromosomes = chromosome_gen(pop, sources);\n\n\nvector = zeros(24, num_sources);    % Best Chromosome Initialization Vector\necon = zeros(24, 1);                % Initialize vector for economic factors\nenviro = zeros(24, 1);              % Environment initialization vector\ntime = zeros(24, 1);                % Vector of storage times\nfor i = 1:length(load)\n    tic;\n\n    % Obtain fitness vector\n    fit = fitness(chromosomes, sources, boundaries, weights, load(i));\n    [best, best_i] = min(fit);\n\n    % Loop until a suitable chromosome is found\n    while(~stop_condition(fit, good_enough))\n\n        % Selected method of reproduction\n        chromosomes = reproduction(chromosomes, pop, sources, boundaries, m_rate, c_pt);\n        fit = fitness(chromosomes, sources, boundaries, weights, load(i));\n\n        % Survival\n        chromosomes = survival(pop, chromosomes, fit);\n\n        % Fitness\n        fit = fitness(chromosomes, sources, boundaries, weights, load(i));\n        [best,best_i]=min(fit);\n        \n        % Remove NaN\n        if(isnan(best))\n            best = 1;\n        end\n    end\n\n    %Store the time that has passed\n    elapsed = toc; \n    time(i) = elapsed;\n\n    % Store the chromosomes in a vector\n    vector = store_best(vector, fit, chromosomes, i);\n    \n    % Storage Economic Factors\n    econ(i) = econ_fitness(chromosomes(best_i, :), sources, boundaries, weights);\n\n    % Store environmental factors\n    enviro(i) = enviro_fitness(chromosomes(best_i, :), sources, boundaries, weights);\nend\n\n%% Visualization\nenviro_plot(enviro);\necon_plot(econ);\npower_plot(vector, load);\ncalculation_plot(time);\n\n%% Output\nget_data(load, vector, sources)\n  
​  

## Images

![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](02.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](03.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](04.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](05.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](06.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](07.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](08.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](09.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](10.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](11.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](12.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](13.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](14.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](15.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](16.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](17.png)
![Improving Genetic Algorithms for Optimizing Microgrid Scheduling (Considering Environmental Factors)](18.png)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
