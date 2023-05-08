Download Link: https://assignmentchef.com/product/solved-se465-assignment-3
<br>
<h1>Question 1</h1>

A few months ago, I wrote an automarker for your Assignment 1 Question 1 submissions. You will know enough to write this automarker yourself. We’ll focus on just the technically challenging part.

I’ve included PMD in the a3 skeleton and provided a template PMD <sub>a1q1-automarker.xml </sub>file. Use the following command in your VM to run your automarker:

~/shared/pmd/bin/run.sh pmd -f text -d ~/shared/q1/A1Q1Test.java -R ~/shared/q1/a1q1-automarker.xml

Your task is to write a PMD rule that detects JUnit 4 test methods which have no calls to assert methods with arguments named mockCommandSender.getLastMessage. JUnit 4 test methods have a Test annotation. Calls to assert methods are Statements with a PrimaryPrefix descendant whose name starts with “assert”. Submit your a1q1-automarker.xml file in directory q1/.

In file <sub>q1/A1Q1Test.java</sub>, write test methods that show that your query works properly; these tests should show that your query flags methods that it should and doesn’t flag methods that it shouldn’t.

<h1>Question 2</h1>

Recall <sub>icalendarlib </sub>from Assignment 2. I’ve made some changes to it to make it more Valgrind-friendly and again placed it in <sub>shared/icalendarlib</sub>. The code contains 4 memory errors. Using <sub>valgrind</sub>, or otherwise, find the errors and submit the diff for your changes in file <sub>q2/icalendarlib-memory.diff</sub>. I believe that two of the errors are not reachable from the current <sub>main.cpp </sub>file. You’ll need to add more code to <sub>main.cpp </sub>if you want to trigger them.

<h1>Question 3</h1>

In this question, you will critique and improve an existing bug report in Mozilla and write a bug report from scratch.

<ul>

 <li>Read Mozilla bug report 112785 (<a href="https://bugzilla.mozilla.org/show_bug.cgi?id=112785">https://bugzilla.mozilla.org/show_bug.cgi?id=112785</a>). What are some problems with the initial bug report (as seen in the “Title” and the “Description”)? Identify four problems. How would you improve this bug report? (5 points)</li>

 <li>The class <sub>q3/HashTable.java </sub>is an implementation of a hash table using linear open addressing and division in Java. This program has a bug, because the <sub>p</sub>ut function will not update the element associated with the given key if an entry with the same key already exists. The hash table implementation should always update the element, even if the element’s key already exists in the hash table. (See the comment in the <sub>p</sub>ut function).</li>

</ul>

Write a good bug report for this bug using the Bugzilla bug report format. (5 points)

(Recommended exercise, not for marks: write a JUnit test that illustrates this bug.)

<h1>Question 4</h1>

In this question, add unit tests to the com.itextpdf.text.pdf.TaggedPdfTest class for the add(final Element o) method of the com.itextpdf.text.List class from iText (in shared/itext). Your solution must use mock objects (with a mock object library of your choice; modify your <sub>pom.xml </sub>accordingly). Your tests must kill the following mutants:

<strong>public boolean </strong>add(<strong>final </strong>Element o) { <strong>if </strong>(o <strong>instanceof </strong>ListItem) { ListItem item = (ListItem) o;

<strong>if </strong>(numbered || lettered) { <em>// mutant 1: || -&gt; &amp;&amp; </em>Chunk chunk = <strong>new </strong>Chunk(preSymbol, symbol.getFont()); chunk.setAttributes(symbol.getAttributes());

<strong>int </strong>index = first + list.size(); <em>// mutant 2: index = first (NOTE EDIT), mutant 3: list -&gt; item </em><strong>if </strong>( lettered )

chunk.append(RomanAlphabetFactory.getString(index, lowercase));

<strong>else </strong>chunk.append(String.valueOf(index));

chunk.append(postSymbol); item.setListSymbol(chunk);

} <strong>else </strong>{ item.setListSymbol(symbol);

} item.setIndentationLeft(symbolIndent, autoindent); item.setIndentationRight(0); <strong>return </strong>list.add(item); <em>// mutant 4: list -&gt; item</em>

}

<strong>else if </strong>(o <strong>instanceof </strong>List) { List nested = (List) o; nested.setIndentationLeft(nested.getIndentationLeft() + symbolIndent); first–; <strong>return </strong>list.add(nested); <em>// mutant 5: nested -&gt; null</em>

} <strong>return false</strong>;

}

I’m aware that the unit tests that come with iText also kill the mutants. But they don’t use mock objects. As I wrote above, your solutions are required to use mock objects.

Here is an additional hint:

<ol>

 <li>Be aware of the EasyMock factory method <sub>notNull() </sub>and class <sub>Capture&lt;T&gt;</sub>.</li>

</ol>

<h1>Question 5</h1>

In this question, you will perform code review. You may: 1) review your own code from the past; 2) review some code that a friend provides for you; or 3) review code that I suggest, namely the com.itextpdf.text.pdf.SimpleBookmark class from iText (which we saw in Question 4). The advantage of (1) and (2) is that you have the opportunity to get your questions about the code answered. The code may be in any language but should be between 500 and 1000 lines of code. You may also review a pull request of a similar magnitude.

Your task is to apply the code review checklist at <a href="https://jesseheines.com/~heines/91.462/Resources/CodeReviewChecklists/Binder_4documents_2016-03-20.pdf">https://jesseheines.com/~heines/91.462/Resources/CodeReviewChecklists/</a>

<a href="https://jesseheines.com/~heines/91.462/Resources/CodeReviewChecklists/Binder_4documents_2016-03-20.pdf">Binder_4documents_2016-03-20.pdf</a> (formerly at Fog Creek, but that doesn’t seem to be on the Internet anymore.) In particular, pick 3 questions from that list and answer them for the code that you are reviewing. Explain your answer in a couple of sentences, supporting it with examples from the code that you’re reviewing. Put your solution in either file q5/codereview.md (Markdown syntax preferred) or q5/codereview.pdf.