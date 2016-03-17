# ungendered-pronouns
A browser extension that replaced gendered adjectives with gender neutral adjectives
function walk(rootNode)
{
    // Find all the text nodes in rootNode
    var walker = document.createTreeWalker(
        rootNode,
        NodeFilter.SHOW_TEXT,
        null,
        false
    ),
    node;

    // Modify each text node's value
    while (node = walker.nextNode()) {
        handleText(node);
    }
}

function handleText(textNode) {
  textNode.nodeValue = replaceText(textNode.nodeValue);
}

function replaceText(v)
{

    // Shrill
    v = v.replace(/\bShrill\b/g, “Passionate");
    v = v.replace(/\bshrill\b/g, “passionate");

    // Pushy
    v = v.replace(/\bPushy\b/g, “Decisive”);
    v = v.replace(/\bpushy\b/g, “decisive");


    // Frump
    v = v.replace(/\bFrumpy\b/g, “Poorly dressed”);
    v = v.replace(/\bfrumpy\b/g, “poorly dressed”);

    // Emotional
    v = v.replace(/\bEmotional\b/g, “Fired Up”);
    v = v.replace(/\bemotional\b/g, “fired up”);

    // Aggressive 
    v = v.replace(/\bAggressive\b/g, “Passionate”);
    v = v.replace(/\baggressive\b/g, “passionate”);

    // Bimbo
    v = v.replace(/\bBimbo\b/g, “Person”);
    v = v.replace(/\bbimbo\b/g, “person”);

    // Bitch
    v = v.replace(/\bBitch\b/g, “Person”);
    v = v.replace(/\bbitch\b/g, “person”);

    // Whore
    v = v.replace(/\bWhore\b/g, “Person”);
    v = v.replace(/\bwhore\b/g, “person”);

    // Slut
    v = v.replace(/\bSlut\b/g, “Person”);
    v = v.replace(/\bslut\b/g, “person”);

    // Ho
    v = v.replace(/\bHo\b/g, “Person”);
    v = v.replace(/\bho\b/g, “person”);

    // Catfight
    v = v.replace(/\bCatfight\b/g, “Argument”);
    v = v.replace(/\bcatfight\b/g, “argument”);

    // Too Ambitious
    v = v.replace(/\bToo Ambitious\b/g, “Go Getter”);
    v = v.replace(/\btoo ambitious\b/g, “go getter”);

 // Female
    v = v.replace(/\bFemale\b/g, “Human”);
    v = v.replace(/\bfemale\b/g, “human”);

 // Homely
    v = v.replace(/\bHomely\b/g, “Natural”);
    v = v.replace(/\bhomely\b/g, “natural”);


 // Old
    v = v.replace(/\Bold\b/g, “Experienced”);
    v = v.replace(/\bold\b/g, “experienced”);

 // Ugly
    v = v.replace(/\Ugly\b/g, “Smart”);
    v = v.replace(/\ugly\b/g, “smart”);

 // Domineering
    v = v.replace(/\Domineering\b/g, “Go getter”);
    v = v.replace(/\domineering\b/g, “go getter”);

 // Has Balls
    v = v.replace(/\Has Balls\b/g, “Has ovaries”);
    v = v.replace(/\has balls\b/g, “has ovaries”);

 // Has Balls
    v = v.replace(/\Has Balls\b/g, “Has ovaries”);
    v = v.replace(/\has balls\b/g, “has ovaries”);

 // Dictatorial
    v = v.replace(/\Dictatorial\b/g, “Assertive”);
    v = v.replace(/\dictatorial\b/g, “assertive”);

 // Pussy
    v = v.replace(/\Pussy\b/g, “Cautious”);
    v = v.replace(/\pussy\b/g, “cautious”);
 
// Squaw 
    v = v.replace(/\Squaw\b/g, “Person”);
    v = v.replace(/\squaw\b/g, “person”);
 
// The Weaker Sex 
    v = v.replace(/\The Weaker Sex\b/g, “Women”);
    v = v.replace(/\the weaker sex\b/g, “women”);

// Matronly 
    v = v.replace(/\Matronly\b/g, “Experienced”);
    v = v.replace(/\matronly\b/g, “experienced”);

// Old Maid 
    v = v.replace(/\Old Maid\b/g, “Experienced”);
    v = v.replace(/\old maid\b/g, “experienced”);

// Old Bag 
    v = v.replace(/\Old Bag\b/g, “Experienced”);
    v = v.replace(/\old bag\b/g, “experienced”);

// Frigid
    v = v.replace(/\Frigid\b/g, “Serious”);
    v = v.replace(/\frigid\b/g, “serious”);

// Moody
    v = v.replace(/\Moody\b/g, “Appropriately Concerned”);
    v = v.replace(/\moody\b/g, “appropriately concerned”);

// Hysterical
    v = v.replace(/\Hysterical\b/g, “Opinionated”);
    v = v.replace(/hysterical\b/g, “opinionated”);




    return v;
}

// The callback used for the document body and title observers
function observerCallback(mutations) {
    var i;

    mutations.forEach(function(mutation) {
        for (i = 0; i < mutation.addedNodes.length; i++) {
            if (mutation.addedNodes[i].nodeType === 3) {
                // Replace the text for text nodes
                handleText(mutation.addedNodes[i]);
            } else {
                // Otherwise, find text nodes within the given node and replace text
                walk(mutation.addedNodes[i]);
            }
        }
    });
}

// Walk the doc (document) body, replace the title, and observe the body and title
function walkAndObserve(doc) {
    var docTitle = doc.getElementsByTagName('title')[0],
    observerConfig = {
        characterData: true,
        childList: true,
        subtree: true
    },
    bodyObserver, titleObserver;

    // Do the initial text replacements in the document body and title
    walk(doc.body);
    doc.title = replaceText(doc.title);

    // Observe the body so that we replace text in any added/modified nodes
    bodyObserver = new MutationObserver(observerCallback);
    bodyObserver.observe(doc.body, observerConfig);

    // Observe the title so we can handle any modifications there
    if (docTitle) {
        titleObserver = new MutationObserver(observerCallback);
        titleObserver.observe(docTitle, observerConfig);
    }
}
walkAndObserve(document);
