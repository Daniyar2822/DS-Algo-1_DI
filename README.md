# Gale-Shapley algorithm to match students and professors
#### Leticia Figueiredo Collado, Luca-Verona Vellage, Isabella Urbano-Trujillo, Daniyar Imanaliev, Daniel Boppert
#### Spring Semester 2024 - Data Structures & Algorithms final project - Master of Data Science for Public Policy
  
  
Folders: 

1. Code
1.1 algo_stuff  
    Anything that touches on the current state of dev for the inner workings for the gs algorithm.  
    Currently also holds synthetic data creation. This should move from initial "hardcoded" data to an "undefined" structure so it can take the input data frome the flaskapp.  
1.1.1 first_iteration  
     Includes the "naive" implementation for a random allocation and then handles even preferences.
1.1.2 max_spots  
     Handles the allocation when professors have different numbers of spots available.  
1.1.3 unequal_sets  
     Handles the allocation for limited preferences for students and professors, which means students dont rank all professors and viceversa.  

2. Flask_Dynamic
3. Flask_Frontend  
4. Flask_Frontend_final

   

### **Gale–Shapley Algorithm**

The Gale-Shapley algorithm, also known as the stable marriage problem, is a solution for pairing individuals from two sets, such that there are no unstable pairs. It's a fundamental algorithm used in various matching scenarios, like assigning medical students to professors for projects.

**Problem statement**: Consider two sets, A and B, with an equal number of elements, where each element from set A has a preference list ranking the elements of set B, and vice versa. The objective is to find a matching between elements of set A and set B that is stable, meaning there are no two elements who prefer each other over their current partners.
**Stability criteria**: A pair (a, b) is unstable if:
    - Either a prefers b over his/her current partner.
    - Or b prefers a over his/her current partner.
**Preferences**: Each element in set A and set B ranks the elements of the opposite set according to their preference.

**Important points:**

1. The Gale-Shapley algorithm **guarantees finding a stable matching** through its iterative process, ensuring that no two people would prefer each other over their current partners. The mathematical proof of stability and convergence relies on several key properties:
    - **Monotonicity**: Once a proposer is accepted by an acceptor, they can only be rejected for someone better according to the acceptor's preferences. This ensures progress towards stability.
    - **Inevitability of Engagement**: Since the number of proposers and acceptors is equal and preferences are complete (everyone ranks all members of the opposite group), everyone must eventually get engaged, preventing infinite loops.
    - **No Blocking Pairs**: The algorithm prevents the formation of any pair where both members would prefer each other over their current partners. This is because if one prefers another over their current match, it means they must have proposed and been rejected in favor of a more preferred choice.
    - **Termination**: The process terminates when there are no unengaged proposers left, ensuring that a stable matching is found.

Mathematically, the algorithm's design ensures that each step moves the system closer to a stable state without the possibility of creating instabilities, leading to a guaranteed stable matching upon completion.

2. Correctness
To prove the correctness of the Gale-Shapley algorithm, we focus on two main points: it terminates with a stable matching, and it ensures no pair would prefer each other over their current matches, hence no blocking pairs exist.
- **Termination**: The algorithm progresses by having proposers propose to their highest-ranked acceptor to whom they have not yet proposed. Since the number of proposers and acceptors is finite and preferences are strictly ordered, each proposer can only propose a finite number of times before running out of options. Thus, the algorithm must terminate.
- **Stability**: Upon termination, every proposer is matched with an acceptor. Suppose there exists a blocking pair, meaning a proposer and an acceptor prefer each other over their current matches. For this to happen, the proposer must have proposed to the acceptor before their current match (since proposers propose in order of their preference). However, if the acceptor preferred this proposer to their final match, they would not have rejected the proposer, contradicting the assumption of a blocking pair. Therefore, no blocking pair can exist, proving the matching is stable.  
These points together prove the algorithm's correctness: it always terminates and, when it does, yields a stable matching.

3. Efficiency
The Gale-Shapley algorithm is efficient due to its computational complexity, which is *O*(*n*2), where *n* is the number of proposers or acceptors. This efficiency arises because each proposer can propose to each acceptor at most once, and each proposal requires a constant amount of time to process. The algorithm terminates when all proposers are matched, ensuring that the number of steps is bounded by the number of possible proposals. This polynomial-time complexity is what makes the Gale-Shapley algorithm practical for solving large instances of the stable matching problem.


#### Complexity of G-S

**Time-complexity of G-S: *O*(*n^2*)**
- In the beginning 2n entities are initialised  
- Each student proposes their preference at max once  

**Worst-case:**  
- All students have to propose all preferences and professors have to make a decision on all preferences  
- This would require n^2 iterations  

**Constant Time:**   
- Deciding entitiy (’professors’) decide on proposal between (accept new proposal, keep match, reject proposal)  
- Decision-making (by ‘professors’ occurs in constant time because the procedure is always the same —> Comparing two options (proposal vs. own preference list)  

**Quadratic Time:**  
- Initialisation phase: Linear  
- Proposal phase: Quadratic —> the quadratic phase dominates, therefore the overall time complexity of GS is: O(n^2)  

**Assessment:**  
- O(n^2) is not the most efficient time complexity in an absoulte sense, esp. for large datatsets  
- It is relatively efficient fot SMP, esp considering the constraints of (1) stability and (2) mutual preference satisfaction  
- SMP belong to a category of problems for which it has not been proven yet if polynomial time algorithms exist for solving them, therefore GS provides a relatively efficient solution to SMP despite running in quadratic time  

**Deployment**
Application is deployed locally and on the website: https://lfcollado.pythonanywhere.com/ 



