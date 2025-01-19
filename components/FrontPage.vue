<template>
  
  <div class="front-page-container" :style="{ backgroundImage: `url(${require('@/assets/abstract.jpg')})` }">
    <h1 class="roadmap-title">CodeCrafter - Free DSA Roadmap</h1>
    <h4>Time to kickstart your journey to your dream job</h4>
    <div class="concept-links">
      <div 
        v-for="(questions, concept) in questions" 
        :key="concept" 
        class="concept-item"
      >
        <button class="topic-btn" @click="showQuestions(concept)">
          {{ concept }}
        </button>
      </div>
    </div>

    <!-- Pop-Up Questions -->
    <div 
      v-if="selectedConcept" 
      class="popup-overlay" 
      @click="closePopup"
    >
      <div class="popup-content" @click.stop>
        <button class="close-btn" @click="closePopup">×</button>
        <h2>{{ selectedConcept }}</h2>

        <p>{{ checkedCount }}/{{ questions[selectedConcept].length }} completed</p>
        <progress :value="checkedCount" :max="questions[selectedConcept].length"></progress>

        <div class="popup-description">
          <h3>{{ popupDescription[selectedConcept] }}</h3>
        </div>
        <table>
          <thead>
            <tr>
              <th>Problem</th>
              <th>Difficulty</th>
              
              <th>Difficulty Score</th>
              
            </tr>
          </thead>
          <tbody>
            <tr v-for="(question, index) in questions[selectedConcept]" :key="index">
              <td>
                <a :href="question.link" target="_blank">{{ question.name }}</a>
              </td>
              <td>{{ question.difficulty }}</td>
              
              <td>{{ question.difficultyScore }}</td>
              <td>
                <input
                  type="checkbox"
                  v-model="question.completed"
                  @change="updateProgress"
                />
              </td>
            </tr>
          </tbody>
        </table>
        <button class="save-button" @click="saveProgress">Save Progress</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      
      popupDescription: {
        "Arrays": "Master the fundamentals of arrays: manipulation and operations.",
        "Strings": "Work through problems involving character sequences and patterns.",
        "Linked Lists": "Learn about singly and doubly linked lists with various problems.",
        "Stacks": "Build knowledge of stack-based data structures and applications.",
        "Queues": "Understand queue operations, including circular and priority queues.",
        "Trees": "Dive into binary trees, BSTs, and advanced tree structures.",
        "Graphs": "Explore graph traversal algorithms like BFS, DFS, and more.",
        "Dynamic Programming": "Solve optimization problems with DP strategies.",
        "Greedy Algorithms": "Tackle problems with efficient greedy approaches.",
        "Backtracking": "Learn to explore all possibilities via backtracking.",
        "Hashing": "Use hash maps and sets to solve key-value problems.",
        "Bit Manipulation": "Master bit-level operations for advanced problems.",
      },
      questions: {
        "Arrays": [
          { name: "find closest number to zero", link: "https://leetcode.com/problems/find-closest-number-to-zero/", difficulty: "Easy", difficultyScore: 4 },
          {name: "Roman to Integer", link: "https://leetcode.com/problems/roman-to-integer/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Best Time to Buy and Sell Stock", link: "https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/", difficulty: "Easy", difficultyScore: 5},
          {name: "Summary Ranges", link: "https://leetcode.com/problems/summary-ranges/description/", difficulty: "Easy", difficultyScore: 5},
          {name: "Product of Arrays", link: "https://leetcode.com/problems/product-of-array-except-self/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Merge Intervals", link: "https://leetcode.com/problems/merge-intervals/description/", difficulty: "Medium", difficultyScore: 8},
          {name: "Spiral Matrix", link: "https://leetcode.com/problems/spiral-matrix/description/", difficulty: "Medium", difficultyScore: 8},
          {name: "Rotate Image", link: "https://leetcode.com/problems/rotate-image/description/", difficulty: "Medium", difficultyScore: 9},
          {name: "Text justification", link: "https://leetcode.com/problems/text-justification/description/?envType=problem-list-v2&envId=array", difficulty: "Hard", difficultyScore: 9},
          { name: "First Missing Positive", link: "https://leetcode.com/problems/first-missing-positive/description/?envType=problem-list-v2&envId=array", difficulty: "Hard", difficultyScore: 8.7},
          {name: "N-Queens", link: "https://leetcode.com/problems/n-queens/description/?envType=problem-list-v2&envId=array", difficulty: "Hard", difficultyScore: 10}
        ],
        "Strings": [
          { name: "Is Sequence", link: "https://leetcode.com/problems/is-subsequence/description/", difficulty: "Easy", difficultyScore: 4.5 },
          {name: "Longest Common Prefix", link: "https://leetcode.com/problems/longest-common-prefix/description/", difficulty: "Easy", difficultyScore: 5},
          {name: "Merge String Alternately", link: "https://leetcode.com/problems/merge-strings-alternately/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Longest Substring Without Reapting Characters", link: "https://leetcode.com/problems/longest-substring-without-repeating-characters/description/?envType=problem-list-v2&envId=string", difficulty: "Medium", difficultyScore: 7},
          {name: "Longest Palimdromic String", link: "https://leetcode.com/problems/longest-palindromic-substring/description/?envType=problem-list-v2&envId=string", difficulty: "Medium", difficultyScore: 8},
          {name: "Zigzag Conversion", link: "https://leetcode.com/problems/zigzag-conversion/description/?envType=problem-list-v2&envId=string", difficulty: "Medium", difficultyScore: 7},
          {name: "Substring Without Concatenation", link: "https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/?envType=problem-list-v2&envId=string", difficulty: "Medium", difficultyScore: 7},
          {name: "Longest Valid Parentheses", link: "https://leetcode.com/problems/longest-valid-parentheses/description/?envType=problem-list-v2&envId=string", difficulty: "Hard", difficultyScore: 9},
          {name: "Wildcard Matching", link: "https://leetcode.com/problems/wildcard-matching/description/?envType=problem-list-v2&envId=string", difficulty: "Hard", difficultyScore: 9},
          
        ],
        "Hashmaps & Sets": [
          {name: "Contains Duplicates", link: "https://leetcode.com/problems/contains-duplicate/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Randsom Note", link: "https://leetcode.com/problems/ransom-note/description/", difficulty: "Easy", difficultyScore: 5},
          {name: "jewels and Stones", link: "https://leetcode.com/problems/jewels-and-stones/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Valid Anagrams", link: "https://leetcode.com/problems/valid-anagram/description/", difficulty: "Easy", difficultyScore: 4.5},
          {name: "Maximum Number of Balloons", link: "https://leetcode.com/problems/maximum-number-of-balloons/description/", difficulty: "Easy", difficultyScore: 5.5},
          {name: "Two Sum", link: "https://leetcode.com/problems/two-sum/description/", difficulty: "Easy", difficultyScore: 4.5},
          {name: "Valid Sudoko", link: "https://leetcode.com/problems/valid-sudoku/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Group Anagrams", link: "https://leetcode.com/problems/group-anagrams/description/", difficulty: "Medium", difficultyScore: 8},
          {name: "Repeated DNA Sequence", link: "https://leetcode.com/problems/repeated-dna-sequences/description/?envType=problem-list-v2&envId=hash-table", difficulty: "Medium", difficultyScore: 7.6},
          {name: "Longest Consecutive Sequence", link: "https://leetcode.com/problems/longest-consecutive-sequence/description/", difficulty: "Hard", difficultyScore: 8.7},
          {name: "Word Break II", link: "https://leetcode.com/problems/word-break-ii/description/?envType=problem-list-v2&envId=hash-table", difficulty: "Hard", difficultyScore: 9},
          {name: "Max On a Point Line", link: "https://leetcode.com/problems/max-points-on-a-line/description/?envType=problem-list-v2&envId=hash-table", difficulty: "Hard", difficultyScore: 9}
        ],
        "2 Pointers": [
          {name: "Squares of a Sorted Array", link: "https://leetcode.com/problems/squares-of-a-sorted-array/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Reverse String", link: "https://leetcode.com/problems/reverse-string/description/", difficulty: "Easy", difficultyScore: 5},
          {name: "Valid Palimdrome", link: "https://leetcode.com/problems/valid-palindrome/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Two Sum II Input Array is Sorted", link: "https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/", difficulty: "Medium", difficultyScore: 6},
          {name: "#sum", link: "https://leetcode.com/problems/3sum/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Container with the Most Water", link: "https://leetcode.com/problems/container-with-most-water/description/", difficulty: "Medium", difficultyScore: 7},
          { "name": "Trapping Rain Water II", "link": "https://leetcode.com/problems/trapping-rain-water-ii/description/?envType=problem-list-v2", difficulty: "Hard", difficultyScore: 9},
          {name: "Create Maximum Number", link: "https://leetcode.com/problems/create-maximum-number/description/?envType=problem-list-v2&envId=two-pointers", difficulty: "Hard", difficultyScore: 9},
          {name: "Find Median from Data Stream", link: "https://leetcode.com/problems/find-median-from-data-stream/description/?envType=problem-list-v2&envId=two-pointers", difficulty: "Hard", difficultyScore: 9}
        ],
        "Stacks": [
          {name: "baseball Game", link: "https://leetcode.com/problems/baseball-game/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Valid Parentheses", link: "https://leetcode.com/problems/valid-parentheses/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Implement Stack Using Queue", link: "https://leetcode.com/problems/implement-stack-using-queues/description/?envType=problem-list-v2&envId=stack", difficulty: "Easy", difficultyScore: 5},
          {name: "Palimdrome Linked List", link: "https://leetcode.com/problems/palindrome-linked-list/description/?envType=problem-list-v2&envId=stack", difficulty: "Easy", difficultyScore: 5},
          {name: "evaluate ReversePolish Notation", link: "https://leetcode.com/problems/evaluate-reverse-polish-notation/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Dailt Temperatures", link: "https://leetcode.com/problems/daily-temperatures/description/", difficulty: "Medium", difficultyScore: 6},
          {name: "Min Stack", link: "https://leetcode.com/problems/min-stack/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Longest Valid Parentheses", link: "https://leetcode.com/problems/longest-valid-parentheses/description/?envType=problem-list-v2&envId=stack", difficulty: "Hard", difficultyScore: 8},
          {name: "Largest Rectangle in  Histogram", link: "https://leetcode.com/problems/largest-rectangle-in-histogram/description/?envType=problem-list-v2&envId=stack", difficulty: "Hard", difficultyScore: 8},
          {name: "Basic Calculator", link: "https://leetcode.com/problems/basic-calculator/description/?envType=problem-list-v2&envId=stack", difficulty: "Hard", difficultyScore: 9}
        ],
        "Linked List": [
          { name: "Remove Duplicates from Sorted List", link: "https://leetcode.com/problems/remove-duplicates-from-sorted-list/", difficulty: "Easy", difficultyScore: 4 },
          { name: "Reverse Linked List", link: "https://leetcode.com/problems/reverse-linked-list/", difficulty: "Easy", difficultyScore: 5 },
          {name: "Middle of the Linked List", link: "https://leetcode.com/problems/middle-of-the-linked-list/description/", difficulty: "Easy", difficultyScore: 5},
          {name: "Merge Two Sorted Lists", link: "https://leetcode.com/problems/merge-two-sorted-lists/description/", difficulty: "Easy", difficultyScore: 5},
          {name: "Linked List Cycle", link: "https://leetcode.com/problems/linked-list-cycle/description/", difficulty: "Easy", difficultyScore: 7},
          {name: "Remove nth Node from End", link: "https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/", difficulty: "Medium", difficultyScore: 6},
          {name: "Copy List with Random Pointers", link: "https://leetcode.com/problems/copy-list-with-random-pointer/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Merge k Sorted Lists", link: "https://leetcode.com/problems/merge-k-sorted-lists/description/?envType=problem-list-v2&envId=linked-list", difficulty: "Hard", difficultyScore: 8},
          {name: "Reverse Nodes in k Group", link: "https://leetcode.com/problems/reverse-nodes-in-k-group/description/?envType=problem-list-v2&envId=linked-list", difficulty: "Hard", difficultyScore: 8},
          {name: "Design", link: "https://leetcode.com/problems/design-skiplist/description/?envType=problem-list-v2&envId=linked-list", difficulty: "Hard", difficultyScore: 9}
        ],
       
"Binary Search": [
  { name: "Binary Search", link: "https://leetcode.com/problems/binary-search/description/", difficulty: "Easy", difficultyScore: 4 },
  { name: "Search Insert Position", link: "https://leetcode.com/problems/search-insert-position/description/", difficulty: "Easy", difficultyScore: 4 },
  { name: "First Bad Version", link: "https://leetcode.com/problems/first-bad-version/description/", difficulty: "Easy", difficultyScore: 5 },
  { name: "Valid Perfect Square", link: "https://leetcode.com/problems/valid-perfect-square/description/", difficulty: "Easy", difficultyScore: 5 },
  { name: "Search A 2D Matrix", link: "https://leetcode.com/problems/search-a-2d-matrix/description/", difficulty: "Medium", difficultyScore: 7 },
  { name: "Find Minimum In Rotated Sorted Array", link: "https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/", difficulty: "Medium", difficultyScore: 6 },
  { name: "Search In Rotated Sorted Array", link: "https://leetcode.com/problems/search-in-rotated-sorted-array/description/", difficulty: "Medium", difficultyScore: 7 },
  { name: "Koko Eating Bananas", link: "https://leetcode.com/problems/koko-eating-bananas/description/", difficulty: "Medium", difficultyScore: 8 },
  { name: "Median Of Two Sorted Arrays", link: "https://leetcode.com/problems/median-of-two-sorted-arrays/description/?envType=problem-list-v2&envId=binary-search", difficulty: "Hard", difficultyScore: 8 },
  { name: "Find Minimum In Rotated Sorted Array II", link: "https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/description/?envType=problem-list-v2&envId=binary-search", difficulty: "Hard", difficultyScore: 9 }
],
"Sliding Window": [
  { name: "Maximum Average Subarray I", link: "https://leetcode.com/problems/maximum-average-subarray-i/description/", difficulty: "Easy", difficultyScore: 4 },
  { name: "Max Consecutive Ones III", link: "https://leetcode.com/problems/max-consecutive-ones-iii/description/", difficulty: "Easy", difficultyScore: 4 },
  { name: "Max Consecutive Ones III", link: "https://leetcode.com/problems/max-consecutive-ones-iii/description/", difficulty: "Easy", difficultyScore: 5 },
  { name: "Longest Substring Without Repeating Characters", link: "https://leetcode.com/problems/longest-substring-without-repeating-characters/description/", difficulty: "Easy", difficultyScore: 5 },
  { name: "Longest Repeating Character Replacement", link: "https://leetcode.com/problems/longest-repeating-character-replacement/description/", difficulty: "Medium", difficultyScore: 7 },
  { name: "Minimum Size Subarray Sum", link: "https://leetcode.com/problems/minimum-size-subarray-sum/description/", difficulty: "Medium", difficultyScore: 6 },
  { name: "Permutation In String", link: "https://leetcode.com/problems/permutation-in-string/description/", difficulty: "Medium", difficultyScore: 7 },
  { name: "Substring With Concatenation Of All Words", link: "https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/?envType=problem-list-v2&envId=sliding-window", difficulty: "Hard", difficultyScore: 8 },
  { name: "Minimum Window Substring", link: "https://leetcode.com/problems/minimum-window-substring/description/?envType=problem-list-v2&envId=sliding-window", difficulty: "Hard", difficultyScore: 8 },
  { name: "Contains Duplicate III", link: "https://leetcode.com/problems/contains-duplicate-iii/description/?envType=problem-list-v2&envId=sliding-window", difficulty: "Hard", difficultyScore: 9 }
],
"Trees": [
  { name: "Diameter Of Binary Tree", link: "https://leetcode.com/problems/diameter-of-binary-tree/description/", difficulty: "Easy", difficultyScore: 4 },
  { name: "Maximum Depth Of Binary Tree", link: "https://leetcode.com/problems/maximum-depth-of-binary-tree/description/", difficulty: "Easy", difficultyScore: 4 },
  { name: "Invert Binary Tree", link: "https://leetcode.com/problems/invert-binary-tree/description/", difficulty: "Easy", difficultyScore: 5 },
  { name: "Implement Trie Prefix Tree", link: "https://leetcode.com/problems/implement-trie-prefix-tree/description/", difficulty: "Easy", difficultyScore: 5 },
  { name: "Lowest Common Ancestor Of A Binary Search Tree", link: "https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/", difficulty: "Medium", difficultyScore: 7 },
  { name: "Validate Binary Search Tree", link: "https://leetcode.com/problems/validate-binary-search-tree/description/", difficulty: "Medium", difficultyScore: 6 },
  { name: "Subtree Of Another Tree", link: "https://leetcode.com/problems/subtree-of-another-tree/description/", difficulty: "Medium", difficultyScore: 7 },
  { name: "Binary Tree Level Order Traversal", link: "https://leetcode.com/problems/binary-tree-level-order-traversal/description/", difficulty: "Hard", difficultyScore: 8 },
  { name: "Kth Smallest Element In A BST", link: "https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/", difficulty: "Hard", difficultyScore: 8 }
],
"Heaps": [
  { name: "Last Stone Weight", link: "https://leetcode.com/problems/last-stone-weight/description/", difficulty: "Easy", difficultyScore: 4 },
  { name: "Relative Ranks", link: "https://leetcode.com/problems/relative-ranks/description/?envType=problem-list-v2&envId=heap-priority-queue", difficulty: "Easy", difficultyScore: 4 },
  { name: "Kth Largest Element In A Stream", link: "https://leetcode.com/problems/kth-largest-element-in-a-stream/description/?envType=problem-list-v2&envId=heap-priority-queue", difficulty: "Easy", difficultyScore: 5 },
  { name: "Kth Largest Element In An Array", link: "https://leetcode.com/problems/kth-largest-element-in-an-array/description/", difficulty: "Medium", difficultyScore: 7 },
  { name: "Top K Frequent Elements", link: "https://leetcode.com/problems/top-k-frequent-elements/description/", difficulty: "Medium", difficultyScore: 6 },
  { name: "K Closest Points To Origin", link: "https://leetcode.com/problems/k-closest-points-to-origin/description/", difficulty: "Medium", difficultyScore: 7 },
  { name: "Merge K Sorted Lists", link: "https://leetcode.com/problems/merge-k-sorted-lists/description/", difficulty: "Hard", difficultyScore: 8 }
],

        "Recursive Backtracking": [
          {name: "Binary Tree Paths", link: "https://leetcode.com/problems/binary-tree-paths/description/?envType=problem-list-v2&envId=backtracking", difficulty: "Easy", difficultyScore: 4},
          {name: "Binary Watch", link: "https://leetcode.com/problems/binary-watch/description/?envType=problem-list-v2&envId=backtracking", difficulty: "Easy", difficultyScore: 4},
          {name: "Sum of all Subset XOR Totals", link: "https://leetcode.com/problems/sum-of-all-subset-xor-totals/description/?envType=problem-list-v2&envId=backtracking", difficulty: "Easy", difficultyScore: 5},
          {name: "Subsets", link: "https://leetcode.com/problems/subsets/description/", difficulty: "Medium", difficultyScore: 5},
          {name: "Permutation", link: "https://leetcode.com/problems/permutations/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Combinations", link: "https://leetcode.com/problems/combinations/description/", difficulty: "Medium", difficultyScore: 6},
          {name: "Word Search", link: "https://leetcode.com/problems/word-search/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Sudoko Solver", link: "https://leetcode.com/problems/sudoku-solver/description/?envType=problem-list-v2&envId=backtracking", difficulty: "Hard", difficultyScore: 8},
          {name: "N Queens", link: "https://leetcode.com/problems/n-queens/description/?envType=problem-list-v2&envId=backtracking", difficulty: "Hard", difficultyScore: 8},
          {name: "N Queens II", link: "https://leetcode.com/problems/n-queens-ii/description/?envType=problem-list-v2&envId=backtracking", difficulty: "Hard", difficultyScore: 9}
        ],
        "Graphs ": [
          {name: "Find if Path Exists in Graph", link: "https://leetcode.com/problems/find-if-path-exists-in-graph/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Number of Island", link: "https://leetcode.com/problems/number-of-islands/description/", difficulty: "Medium", difficultyScore: 4},
          {name: "Max Area of Island", link: "https://leetcode.com/problems/max-area-of-island/description/", difficulty: "Medium", difficultyScore: 5},
          {name: "course Schedule", link: "https://leetcode.com/problems/course-schedule/description/", difficulty: "Medium", difficultyScore: 5},
          {name: "Pacific Atlantic Water Flow", link: "https://leetcode.com/problems/pacific-atlantic-water-flow/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Course Schedule II", link: "https://leetcode.com/problems/course-schedule-ii/description/", difficulty: "Medium", difficultyScore: 6},
          {name: "Clone Graph", link: "https://leetcode.com/problems/clone-graph/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Rotting Oranges", link: "https://leetcode.com/problems/rotting-oranges/description/", difficulty: "Medium", difficultyScore: 8},
          {name: "Min Cost to Connect all Points", link: "https://leetcode.com/problems/min-cost-to-connect-all-points/description/", difficulty: "Medium", difficultyScore: 8},
          {name: "Network Delay Time", link: "https://leetcode.com/problems/network-delay-time/description/", difficulty: "Medium", difficultyScore: 9}
        ],
         "Dynamic Programming ": [
          {name: "Fibonacci Number", link: "https://leetcode.com/problems/fibonacci-number/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Climbing Stairs", link: "https://leetcode.com/problems/climbing-stairs/description/", difficulty: "Easy", difficultyScore: 4},
          {name: "Min Cost Climbing Stairs", link: "https://leetcode.com/problems/min-cost-climbing-stairs/description/", difficulty: "Easy", difficultyScore: 5},
          {name: "House Robber", link: "https://leetcode.com/problems/house-robber/description/", difficulty: "Medium", difficultyScore: 5},
          {name: "Unique Paths", link: "https://leetcode.com/problems/unique-paths/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Maximum Subarray", link: "https://leetcode.com/problems/maximum-subarray/description/", difficulty: "Medium", difficultyScore: 6},
          {name: "Jump Game", link: "https://leetcode.com/problems/jump-game/description/", difficulty: "Medium", difficultyScore: 7},
          {name: "Coin Change", link: "https://leetcode.com/problems/coin-change/description/", difficulty: "Medium", difficultyScore: 8},
          {name: "Longest Increasing Subsequence", link: "https://leetcode.com/problems/longest-increasing-subsequence/description/", difficulty: "Medium", difficultyScore: 8},
          
        ]
      },
      selectedConcept: null,
      checkedCount: 0,
    };
  },
  methods: {
    showQuestions(concept) {
      this.selectedConcept = concept;
    },
    closePopup() {
      this.selectedConcept = null;
    },
    updateProgress() {
      if (this.selectedConcept) {
        this.checkedCount = this.questions[this.selectedConcept].filter(
          (q) => q.completed
        ).length;
      }
    },
    saveProgress() {
      if (this.selectedConcept) {
        const progressData = this.questions[this.selectedConcept].map((q) => ({
          name: q.name,
          completed: q.completed,
        }));
        console.log("Saved progress for", this.selectedConcept, ":", progressData);
        alert("Progress saved successfully!");
      }
    },
  },
};
</script>

<style scoped>

/* General Styles */
.front-page-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fff;
  min-height: 100vh;
  padding: 20px;
  display: flex;
  flex-direction: column;
  background-size: cover; /* Ensures the image covers the container */
  
  color: white; /* Text color for visibility */
  
}

.roadmap-title {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 20px;
}

/* Vertical Concept Links */
.concept-links {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

.concept-item {
  width: 100%;
  text-align: center;
}

.topic-btn {
  background-color: #333;
  color: white;
  border: none;
  border-radius: 6px;
  padding: 15px 30px;
  font-size: 16px;
  cursor: pointer;
  transition: transform 0.2s, background-color 0.2s;
}

.topic-btn:hover {
  background-color: #444;
  transform: scale(1.05);
}

/* Pop-Up Styling */
.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.popup-content {
  background-color: #2c2c2c;
  padding: 20px;
  border-radius: 12px;
  width: 90%;
  max-width: 600px;
  max-height: 80vh;
  overflow-y: auto;
  position: relative;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  color: white;
  font-size: 24px;
  cursor: pointer;
}

.popup-content h2 {
  margin-bottom: 10px;
  text-align: center;
}

.popup-description h3 {
  color: #bbb;
  margin: 10px 0;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

th, td {
  padding: 10px;
  text-align: left;
  border-bottom: 1px solid #444;
}

th {
  background-color: #444;
  color: #fff;
}

.solution-link, .code-link {
  color: white;
  text-decoration: none;
}

.solution-link:hover, .code-link:hover {
  text-decoration: underline;
}
td a {
  color: white; /* Set the link color to light green */
  text-decoration: none; /* Remove underline */
}

td a:hover, td a:active {
  color: lightgreen; /* Ensure the hover and active states remain light green */
  text-decoration: underline; /* Optionally add underline on hover */
}

.questionnaire-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.question-item {
  margin-bottom: 10px;
  font-size: 18px;
}

.progress-container {
  margin: 20px 0;
}

progress {
  width: 100%;
  height: 20px;
  border-radius: 10px;
  overflow: hidden;
}

.save-button {
  display: block;
  width: 30%;
  padding: 8px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  align: center;
}

.save-button:hover {
  background-color: #45a049;
}

</style>
 