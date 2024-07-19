

Accessibility in React

20%
of the global population has a permanent disability and
in our aging population, a further 20% have a progressive impairment


Perceivable
Operable
Understandable
Robust
All users should be able to accurately see and read your website content. That means content must not exclude people with vision loss, hearing loss and other disabilities.
Website content should be responsive and simple to navigate for all users, for example, using only keyboard commands to navigate a website rather than a mouse.
Website interfaces and information should be organised in a way that makes them easy to use, predictable to navigate and contain language that is understandable to all users.
Websites should be compatible with a wide range of technology, including assistive technology tools that are commonly used by users with disabilities.

Does React make accessibility easier or harder?
Yes!

It’s easier to accidentally not support accessibility with React, so there must be intentionality behind decisions. 

If you use accessibility well it can be a great experience for developers and end users.

Quick side note: Principle 4 Robust

To keep things robust, every component needs a…

Name
Will take content inside components unless overwritten
Use aria-label only when there is no visible label
Name is calculated using the Accessible Name and Description Computation 1.2
Always provide unique link names
Use visually hidden (or ‘screen reader only’ text) to provide context for screen reader users
Use relational HTML elements and attributes such as <label>, <fieldset>, scope

Role
Use semantic HTML
Follow specification from the ARIA Authoring Practices Guide (APG)
Use the role attribute where a component deviates from HTML spec
Do not create redundancy in roles
Always ensure the right element is being used; link vs. button, checkbox vs. switch, to name a few
Ensure keyboard interaction work as expected

Value
This includes the state, any properties, and its value
For example, a tab may have a state of disabled, a property of selected, and value 1 of 4
A combination of HTML attributes, aria- type attributes, and relationship to semantics will calculate an element’s value
Think about which props you may need to define as required.


Case study: Sign up form

<form>
<label>
<div>Email address</div>
<input />
</label>
<label>
<div>Password</div>
<input />
</label>
<button>Sign up</button>
</form>
💡Perceivable tip 
Use semantic HTML!

function InputField(props) {
	return (
		<label>
			<div />
			<input />
		</label>
	)
}


function InputField({
labelText
}) {
	return (
		<label>
			<div />
			<input />
		</label>
	)
}


function InputField({
labelText
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input />
		</label>
	)
}

💡Perceivable tip
Programmatically associate form inputs with their labels

function InputField({
labelText,
inputType
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input />
		</label>
	)
}


function InputField({
labelText,
inputType
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType} />
		</label>
	)
}

💡Understandable tip
Use HTML5 types to prevent users making errors

function SignUpForm(props) {
	return (
<form>
<label>
<div>Email address</div>
<input />
</label>
<label>
<div>Password</div>
<input />
</label>
<button>Sign up</button>
</form>
	)
}

function SignUpForm(props) {
	return (
<form>
<InputField />
<InputField />
<button>Sign up</button>
</form>
	)
}

function SignUpForm(props) {
	return (
<form>
<InputField 
labelText=”Email”
/>
<InputField
labelText=”Password” />
<button>Sign up</button>
</form>
	)
}

function SignUpForm(props) {
	return (
<form>
<InputField 
labelText=”Email”
inputType=”email” />
<InputField
labelText=”Password”
inputType=”password” />
<button>Sign up</button>
</form>
	)
}

function SignUpForm(props) {
	return (
<form>
<InputField 
labelText=”Email”
inputType=”email” />
<InputField
labelText=”Password”
inputType=”password” />
<button>Sign up</button>
</form>
	)
}
Component reusability
😄

function InputField({
labelText,
inputType
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType} />
		</label>
	)
}


function InputField({
labelText,
inputType
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType} />
		</label>
	)
}

InputField.propTypes = {
	labelText: PropTypes.string.isRequired
}

function InputField({
labelText,
inputType
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType} />
		</label>
	)
}

InputField.propTypes = {
	labelText: PropTypes.string.isRequired,
inputType: PropTypes.oneOf([`text`, `email`, `password`])
}

function InputField({
labelText,
inputType
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType} />
		</label>
	)
}

InputField.propTypes = {
	labelText: PropTypes.string.isRequired,
inputType: PropTypes.oneOf([`text`, `email`, `password`])
}
PropType
enforcement
😄

function InputField({
labelText,
inputType
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType}/>
		</label>
	)
}


function InputField({
labelText,
inputType,
errorText
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType} />
			{errorText && (
				<div>⚠️ {errorText}</div>
)}
		</label>
	)
}

💡Understandable tip
Link error messages with input labels

function InputField({
labelText,
inputType,
errorText
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType}
aria-invalid={
errorText ? “true” : undefined
} />
			{errorText && (
				<div>⚠️ {errorText}</div>
)}
		</label>
	)
}


function InputField({
labelText,
inputType,
errorText
}) {
	return (
		<label>
			<div>{labelText}</div>
			<input type={inputType}
aria-invalid={
errorText ? “true” : undefined
} />
			{errorText && (
				<div>⚠️ {errorText}</div>
)}
		</label>
	)
}

Adding logic within HTML
😄

function SignUpForm(props) {
	return (
<form>
<InputField 
labelText=”Email”
inputType=”email”
errorText=”Email is required” />
<InputField
labelText=”Password”
inputType=”password” />
<button>Sign up</button>
</form>
	)
}

function SignUpForm(props) {
	return (
<form>
<InputField 
labelText=”Email”
inputType=”email”
errorText=”Email is required” />
<InputField
labelText=”Password”
inputType=”password” />
<button>Sign up</button>
</form>
	)
}
Accessing DOM elements of other components and focus handling 
🤯

Remember our useRef hook?
We can also use forwardRef in our component to expose a DOM node to parent component with a ref.
forwardRef hook

A few other things

Manage focus into components with the useRef hook and forwardRef API, especially important for keyboard or screen-reader users
It is very important in a Single Page Application to manage focus well, such as through setting focus to a container or heading (remember to add tabindex=”-1”), or even keep track of and restoring focus when returning to previous content
Consider focus management when setting up React Router, if needed to change from the default
Make sure focus is locked intentionally but not unexpectedly, good example are in modals
Focus management
💡Operable tip
A logical focus order must be managed for keyboard users when navigating pages or interacting with the UI
With the ever-changing DOM, focus can be lost, so ensure to nudge or reset focus back when things change

You can create variable elements to make semantics more contextual and suitable for the use case or the current state
There is a hook called useContext - one for further reading!
Can be used to understand heading level context if we do not know where a component might be used
Variable elements
function Heading({ children }) {
const level = useContext(LevelContext);
const H = `h${level}`;
return (
<H>{children}</H>
);
}


Use the hook useID to generate a unique ID for a component, important when using attributes such as aria-describedby
Can help add extra accessible information which keeps within a component and avoids the developer needing to worry
Can pass in an additional ID prop as optional if needed to be defined for unit testing, and fall back to the useID generated one if not present
useID hook
function IdExample({ id }) {
const generatedId = useId();
const uid = id ?
id : generatedId;
const titleId = `title-${uid}`;
return (...);
}

React modifies the DOM, just like JavaScript, so any changes inside a component will be announced to screen readers if it is a live region (such as role=”alert”) without having to move keyboard focus
Live regions

{errorText && (
	<div role=”alert”>⚠️ {errorText}</div>
}


Don’t forget to set your document title everytime you go to a new page, even if it is a ‘Single page application’ - use useEffect hook in functional components
Titles work best where the most unique and granular part of the page is at the beginning, and the highest level is at the end of the title, e.g. “Our History - About  - Company”, not the other way around..
Document title
function PageTitle() {
  useEffect(() => {
    document.title = 'My Page Title';
  }, []);
}

To recap

🤯 Difficulties
Accessing DOM elements of other components
Focus handling
Knowing context or where an element might be used
😄 Niceties
Component reusability
PropType enforcement
Adding logic within HTML
Variable element semantics
ID generation for ARIA usage

Use a linter such as eslint-plugin-jsx-a11y to help prevent potential accessibility issues before they go into production, such as
Attribute misspelling or incorrectly applied
ARIA prop validation
Keyboard shortcuts for elements with event listeners
Labelling form fields
… many others
Accessibility tooling

React docs on accessibility (legacy)
Web Content Accessibility Guidelines (WCAG) 2.2
MDN web docs on Accessibility in React
eslint-plugin-jsx-a11y
Resources
