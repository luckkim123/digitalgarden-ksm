---
{"dg-publish":true,"permalink":"/3-archive/et-cs/taskido/todo-list/","noteIcon":""}
---


<style scope=" ">.tasksCalendar span {
	display: contents;
}
.tasksCalendar .buttons {
	cursor: default;
	width: 100%;
	height: 30px;
	display: flex;
	flex-wrap: nowrap;
	flex-direction: row;
	margin-bottom: 4px;
}
.tasksCalendar[view='list'] button.listView,
.tasksCalendar[view='week'] button.weekView,
.tasksCalendar[view='month'] button.monthView,
.tasksCalendar.filter button.filter {
	background: var(--background-modifier-active-hover);
}
body:not(.is-mobile) .tasksCalendar button.listView:hover,
body:not(.is-mobile) .tasksCalendar button.weekView:hover,
body:not(.is-mobile) .tasksCalendar button.monthView:hover,
body:not(.is-mobile) .tasksCalendar button.previous:hover,
body:not(.is-mobile) .tasksCalendar button.next:hover,
body:not(.is-mobile) .tasksCalendar button.current:hover,
body:not(.is-mobile) .tasksCalendar button.filter:hover,
body:not(.is-mobile) .tasksCalendar button.statistic:hover {
	background: var(--background-modifier-hover);
}
.tasksCalendar[view='list'] button.listView svg,
.tasksCalendar[view='month'] button.monthView svg,
.tasksCalendar[view='week'] button.weekView svg,
.tasksCalendar.filter button.filter svg {
	stroke: var(--icon-color-active) !important;
}
.tasksCalendar button {
	background-color: transparent;
	display: inline-flex;
	align-items: center;
	justify-content: center;
	cursor: pointer;
	border-radius: 5px;
	color: var(--icon-color);
	height: 30px;
	box-shadow: none;
	border: 1px solid var(--nav-item-background-active);
	font-weight: normal;
	font-size: 14px;
	background: var(--background-secondary);
	padding: 4px 6px;
	outline: none;
	user-select: none;
	white-space: nowrap;
	flex: 0;
}
.tasksCalendar button:nth-child(2),
.tasksCalendar button:nth-child(3),
.tasksCalendar button:nth-child(6) {
	border-top-right-radius: 0;
	border-bottom-right-radius: 0;
	border-right: 0.5px solid var(--nav-item-background-active);
	margin-right: 0;
}
.tasksCalendar button:nth-child(3),
.tasksCalendar button:nth-child(4),
.tasksCalendar button:nth-child(7) {
	border-top-left-radius: 0;
	border-bottom-left-radius: 0;
	border-left: 0.5px solid var(--nav-item-background-active);
	margin-left: 0;
}
.tasksCalendar .current {
	margin: 0 4px;
	display: inline;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
	flex: 1;
}
.tasksCalendar .current span:first-child {
	font-weight: bold;
	color: var(--icon-color);
}
.tasksCalendar .current span:last-child {
	font-weight: normal;
	color: var(--icon-color-active);
}
.tasksCalendar button:nth-child(1) {
	margin-right: 4px;
}
.tasksCalendar button:nth-child(8) {
	margin-left: 4px;
}
.tasksCalendar svg {
	height: var(--icon-size);
	width: var(--icon-size);
	stroke-width: var(--icon-stroke);
}
.tasksCalendar .statisticPopup,
.tasksCalendar .weekViewContext {
	display: none;
	border-radius: 5px;
	font-size: 10px;
	border: 1px solid var(--nav-item-background-active);
	position: absolute;
	height: auto;
	width: 150px;
	width: auto;
	background: var(--icon-color);
	margin: 0 !important;
	list-style: none;
	padding: 2px !important;
	z-index: 99;
	box-shadow: 0px 0px 10px 0px var(--nav-item-background-active);
	background: var(--background-secondary);
}
.tasksCalendar .statisticPopup {
	right: 0;
}
.tasksCalendar .weekViewContext {
	left: 65px;
}
.tasksCalendar .statisticPopup:before,
.tasksCalendar .weekViewContext:before {
	content: "";
	width: 0px;
	height: 0px;
	-webkit-transform:rotate(360deg);
	border-style: solid;
	border-width: 0 10px 10px 10px;
	border-color: transparent transparent var(--background-secondary) transparent;
	position: absolute;
}
.tasksCalendar .statisticPopup:before {
	top: -10px;
	right: 5px;
}
.tasksCalendar .weekViewContext:before {
	top: -10px;
	left: 5px;
}
.tasksCalendar .statisticPopup.active,
.tasksCalendar .weekViewContext.active {
	display: block;
}
.tasksCalendar .statisticPopup li,
.tasksCalendar .weekViewContext li {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	align-items: center;
	height: auto;
	font-size: 14px;
	list-style: none;
	color: var(--text-normal);
	padding: 5px 10px;
	border-radius: 5px;
	cursor: pointer;
}
.tasksCalendar .statisticPopup li.active,
.tasksCalendar .weekViewContext li.active {
	background: var(--background-modifier-active-hover);
	color: var(--icon-color-active) !important;
}
body:not(.is-mobile) .tasksCalendar .statisticPopup li:not(.active):hover,
body:not(.is-mobile) .tasksCalendar .weekViewContext li:not(.active):hover {
	background: var(--background-modifier-hover);
}
.tasksCalendar .statisticPopup li.break,
.tasksCalendar .weekViewContext li.break {
	height: 1px !important;
	background: var(--nav-item-background-active);
	margin: 2px 5px !important;
	border-radius: 0 !important;
	padding: 0 !important;
}
.tasksCalendar .statisticPopup > div,
.tasksCalendar .weekViewContext > div {
	height: 13px;
	margin: auto 0;
}
.tasksCalendar button.statistic {
	position: relative;
}
.tasksCalendar button.statistic svg {
	stroke: var(--icon-color);
}
.tasksCalendar button.statistic[data-percentage="100"]:after {
	display: none !important;
}
.tasksCalendar button.statistic:after {
	content: attr(data-remaining);
	position: absolute;
	height: 14px;
	width: 14px;
	top: -8px;
	right: -8px;
	border-radius: 50%;
	text-align: center;
	line-height: 14px;
	font-size: 9px;
	font-weight: bold;
	border: 1px solid var(--nav-item-background-active);
	overflow: hidden;
	color: var(--icon-color);
	background: var(--background-secondary);
}
.tasksCalendar .weekViewContext .liIcon {
	display: grid !important;
	height: 18px;
	width: 18px;
	margin-right: 5px;
	padding: 2px;
}
.tasksCalendar .weekViewContext .liIcon .box {
	background: var(--icon-color);
	z-index: 1;
	display: grid;
	overflow: hidden;
	margin: 0.5px;
	border-radius: 1px;
}
.tasksCalendar .weekViewContext li.active .liIcon .box {
	background: var(--icon-color-active) !important;
}
.tasksCalendar .grid {
	overflow: hidden;
	cursor: default;
	width: 100%;
	height: 75vH;
}
.tasksCalendar .list {
	overflow-x: hidden;
	overflow-y: auto;
	cursor: default;
	width: 100%;
	height: 75vH;
}
.tasksCalendar .cell {
	z-index: 1;
	display: grid;
	grid-template-rows: auto 1fr;
	grid-template-columns: 1fr;
	overflow: hidden;
	margin: 1px 0;
}
.tasksCalendar .cellContent {
	overflow-x: hidden;
	overflow-y: auto;
	align-content: start;
	padding: 1px 0;
}
.tasksCalendar .cellContent::-webkit-scrollbar {
	display: none;
}
.tasksCalendar .cellName {
	display: block;
	font-weight: normal;
	padding: 0 2px;
	color: var(--text-normal);
	flex-shrink: 0;
	flex-grow: 0;
	white-space: nowrap;
	text-overflow: ellipsis;
	overflow: hidden;
	text-align: left;
	margin: 0;
	font-size: 14px;
	opacity: 0.8;
}
body:not(.is-mobile) .tasksCalendar .cellName:hover {
	opacity: 1;
}
.tasksCalendar .task {
	overflow: hidden;
	padding: 1px;
	background: var(--task-background);
	border-radius: 3px;
	overflow: hidden;
	margin: 1px 1px 2px 1px;
	font-size: 14px;
	opacity: 0.8;
	display: block;
}
body.theme-dark .tasksCalendar .task { color: var(--light-task-text-color); }
body.theme-light .tasksCalendar .task { color: var(--dark-task-text-color); }
body.theme-dark .tasksCalendar .task .note { color: var(--light-task-text-color); }
body.theme-light .tasksCalendar .task .note { color: var(--dark-task-text-color); }
body:not(.is-mobile) .tasksCalendar .task:hover {
	opacity: 1;
}
.tasksCalendar .task.hide {
	opacity: 0.2;
}
.tasksCalendar .task .inner {
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 1;
	-webkit-box-orient: vertical;
	text-decoration: none;
	word-break: break-all !important;
	-webkit-hyphens: none !important;
	line-height: 1.3;
	text-decoration: none !important;
	border-radius: 3px;
	overflow: hidden;
}
.tasksCalendar a {
	text-decoration: none !important;
}
.tasksCalendar .task .note {
	display: block;
	width: 100%;
	font-size: 9px;
	background: var(--task-background);
	padding: 1px;
	text-overflow: ellipsis;
	overflow: hidden;
	white-space: nowrap;
}
.tasksCalendar .task .icon {
	display: inline;
	width: 18px;
	height: 18px;
	text-align: center;
	margin-right: 3px;
}
.tasksCalendar .task .description {
	display: inline;
	padding: 1px;
}
.tasksCalendar .task .description:before {
	display: inline;
	content: attr(data-relative);
	margin-right: 3px;
	border-radius: 3px;
	margin-right: 3px;
	padding: 0 3px;
	font-size: 9px;
	vertical-align: middle;
}
.tasksCalendar .task.overdue .description:before {
	color: white;
	background: #ff443a;
}
.tasksCalendar .task:not(.overdue) .description:before {
	display: none;
	background: black;
	color: white;
}
.tasksCalendar .task.dailyNote .description:before,
.tasksCalendar .task.done .description:before,
.tasksCalendar .task.cancelled .description:before {
	display: none !important;
}
.tasksCalendar .task.cancelled .note,
.tasksCalendar .task.done .note {
	background: var(--nav-item-background-active) !important;
	color: var(--text-faint) !important;
}
.tasksCalendar .task.cancelled .description,
.tasksCalendar .task.done .description {
	text-decoration: line-through !important;
	color: var(--text-faint) !important;
}
.tasksCalendar .task.cancelled,
.tasksCalendar .task.done {
	background: none !important;
}
.tasksCalendar .task.overdue .inner {
	background: repeating-linear-gradient(45deg, var(--task-background), var(--task-background) 5px, transparent 5px, transparent 10px) !important;
}


/* Today & Weekends */
.tasksCalendar .cell.today .cellName {
	font-weight: bold;
	color: var(--text-normal);
	opacity: 1;
}
.tasksCalendar .cell[data-weekday="0"].today .cellName {
	font-weight: bold;
	color: var(--icon-color-active);
	opacity: 1;
}
.tasksCalendar[view='month'] .cell.today {
	background: var(--background-modifier-active-hover) !important;
	border: 1px solid hsla(var(--interactive-accent-hsl), 0.25) !important;
	border-radius: 5px;
}
.tasksCalendar[view='week'] .cell.today {
	background: var(--background-modifier-active-hover) !important;
	border: 1px solid hsla(var(--interactive-accent-hsl), 0.25) !important;
}
.tasksCalendar .cell[data-weekday="0"] .cellName,
.tasksCalendar .gridHead[data-weekday="0"] {
	color: var(--icon-color-active);
}


/* Month View */
.tasksCalendar[view='month'] .grid {
	display: grid;
	gap: 4px;
	grid-template-rows: 20px 1fr !important;
	grid-template-columns: 1fr !important;
}
.tasksCalendar[view='month'] .gridHeads {
	display: grid;
	grid-template-columns: 20px 1fr 1fr 1fr 1fr 1fr 1fr 1fr !important;
	width: 100%;
	height: 20px;
	border: 1px solid var(--nav-item-background-active);
	border-radius: 5px;
}
.tasksCalendar[view='month'] .gridHead {
	display: inline;
	box-sizing: border-box;
	overflow: hidden;
	text-align: center;
	font-weight: bold;
	text-overflow: ellipsis;
	white-space: nowrap;
	margin: 0;
	font-size: 14px;
	height: 20px;
	line-height: 20px;
	font-size: 10px;
}
.tasksCalendar[view='month'] .wrappers {
	display: grid;
	grid-template-rows: repeat(6, calc(100% / 6));
	grid-template-columns: 1fr !important;
	min-height: 0;
	height: calc(100% - 20px);
	gap: 4px 4px;
}
.tasksCalendar[view='month'] .wrappers,
.tasksCalendar[view='week'] .grid {
	position: relative;
}
.tasksCalendar[view='month'] .wrappers:before,
.tasksCalendar[view='week'] .grid:before,
.tasksCalendar[view='list'] .list:before {
	z-index: 0;
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	font-size: 120px;
	font-weight: bold;
	color: var(--background-modifier-active-hover);
}
.tasksCalendar[view='month'] .wrappers:before,
.tasksCalendar[view='list'] .list:before {
	content: attr(data-month);
}
.tasksCalendar[view='week'] .grid:before {
	content: attr(data-week);
}
.tasksCalendar[view='month'] .wrapper {
	z-index: 1;
	display: grid;
	grid-template-rows: 1fr !important;
	grid-template-columns: 22px 1fr 1fr 1fr 1fr 1fr 1fr 1fr !important;
	width: 100%;
	height: 100%;
	border: 1px solid var(--nav-item-background-active);
	border-radius: 5px;
	overflow: hidden;
}
.tasksCalendar[view='month'] .wrapperButton {
	display: flex;
	writing-mode: vertical-lr;
	transform: rotate(180deg);
	background: none;
	text-align: center;
	align-items: center;
	justify-content: center;
	font-size: 10px;
	font-weight: normal;
	color: var(--text-normal);
	color: var(--icon-color-active);
	cursor: pointer;
	width: 100%;
	overflow: hidden;
	/* background: var(--background-primary); */
	background: var(--background-secondary);
}
.tasksCalendar[view='month'] .wrapperButton:hover {
	background: var(--background-modifier-hover);
}
.tasksCalendar[view='month'] .cell {
	margin: 0;
}
.tasksCalendar[view='month'] .prevMonth,
.tasksCalendar[view='month'] .nextMonth {
	background: var(--background-secondary);
}


/* Week view */
.tasksCalendar[view='week'] .grid {
	display: grid;
	gap: 2px 4px;
}
.tasksCalendar[view='week'] .cell {
	border: 1px solid var(--nav-item-background-active);
	border-radius: 5px;
	overflow: hidden;
}


/* List View */
.tasksCalendar[view='list'] .list {
	border: 1px solid var(--nav-item-background-active);
	border-radius: 5px;
}
.tasksCalendar[view='list'] .list .task,
.tasksCalendar[view='list'] .list .task.done,
.tasksCalendar[view='list'] .list .task .note,
.tasksCalendar[view='list'] .list .task.done .note{
	background: transparent !important;
}
.tasksCalendar[view='list'] .list .task .inner {
	display: flex !important;
	flex-direction: row;
	flex-wrap: nowrap;
	padding: 0 10px;
	white-space: nowrap;
}
.tasksCalendar[view='list'] .list .task .note {
	display: inline-block;
	width: 150px;
	flex-shrink: 0;
	flex-grow: 0;
}
.tasksCalendar[view='list'] .list .task .description {
	width: 100%;
	flex-shrink: 1;
	flex-grow: 1;
}
.tasksCalendar[view='list'] .list .task.done .note,
.tasksCalendar[view='list'] .list .task.done .description,
.tasksCalendar[view='list'] .list .task.cancelled .note,
.tasksCalendar[view='list'] .list .task.cancelled .description {
	color: var(--text-faint) !important;
}
.tasksCalendar[view='list'] .list .task .note,
.tasksCalendar[view='list'] .list .task .description {
	color: var(--task-color) !important;
	line-clamp: 0 !important;
	white-space: nowrap !important;
	text-overflow: ellipsis;
	overflow: hidden;
	font-size: 14px;
}
.tasksCalendar summary::marker,
.tasksCalendar summary::-webkit-details-marker {
	display: none !important;
	content: "" !important;
}
.tasksCalendar[view='list'] details.today {
	background: var(--background-modifier-active-hover);
	border: 1px solid hsla(var(--interactive-accent-hsl), 0.25);
}
.tasksCalendar[view='list'] details.today summary {
	font-weight: bold;
	background: none;
}
.tasksCalendar[view='list'] details.today .content {
	margin: 3px;
}
.tasksCalendar[view='list'] details {
	display: block;
	margin: 5px;
	border-radius: 5px;
	overflow: hidden;
	/*background: var(--background-secondary);*/
	border: 1px solid var(--nav-item-background-active);
}
.tasksCalendar[view='list'] summary {
	background: var(--background-secondary);
	padding: 0 10px;
	border-radius: 5px;
}
.tasksCalendar[view='list'] summary span.weekNr {
	font-size: 11px;
	color: var(--text-faint);
}


/* Style classes */
.tasksCalendar[view='week'].style1 .grid, .iconStyle1 { grid-template-columns: repeat(4, 1fr); grid-template-rows: repeat(6, 1fr); }
.tasksCalendar[view='week'].style1 .grid .cell:nth-child(1), .iconStyle1 .box:nth-child(1) { grid-area: 1 / 1 / 3 / 3; }
.tasksCalendar[view='week'].style1 .grid .cell:nth-child(2), .iconStyle1 .box:nth-child(2) { grid-area: 3 / 1 / 5 / 3; }
.tasksCalendar[view='week'].style1 .grid .cell:nth-child(3), .iconStyle1 .box:nth-child(3) { grid-area: 5 / 1 / 7 / 3; }
.tasksCalendar[view='week'].style1 .grid .cell:nth-child(4), .iconStyle1 .box:nth-child(4) { grid-area: 1 / 3 / 3 / 5; }
.tasksCalendar[view='week'].style1 .grid .cell:nth-child(5), .iconStyle1 .box:nth-child(5) { grid-area: 3 / 3 / 5 / 5; }
.tasksCalendar[view='week'].style1 .grid .cell:nth-child(6), .iconStyle1 .box:nth-child(6) { grid-area: 5 / 3 / 6 / 5; }
.tasksCalendar[view='week'].style1 .grid .cell:nth-child(7), .iconStyle1 .box:nth-child(7) { grid-area: 6 / 3 / 7 / 5; }
.tasksCalendar[view='week'].style2 .grid, .iconStyle2 { grid-template-columns: repeat(4, 1fr); grid-template-rows: repeat(6, 1fr); }
.tasksCalendar[view='week'].style2 .grid .cell:nth-child(1), .iconStyle2 .box:nth-child(1)  { grid-area: 1 / 1 / 3 / 3; }
.tasksCalendar[view='week'].style2 .grid .cell:nth-child(3), .iconStyle2 .box:nth-child(3)  { grid-area: 3 / 1 / 5 / 3; }
.tasksCalendar[view='week'].style2 .grid .cell:nth-child(5), .iconStyle2 .box:nth-child(5)  { grid-area: 5 / 1 / 7 / 3; }
.tasksCalendar[view='week'].style2 .grid .cell:nth-child(2), .iconStyle2 .box:nth-child(2)  { grid-area: 1 / 3 / 3 / 5; }
.tasksCalendar[view='week'].style2 .grid .cell:nth-child(4), .iconStyle2 .box:nth-child(4)  { grid-area: 3 / 3 / 5 / 5; }
.tasksCalendar[view='week'].style2 .grid .cell:nth-child(6), .iconStyle2 .box:nth-child(6)  { grid-area: 5 / 3 / 6 / 5; }
.tasksCalendar[view='week'].style2 .grid .cell:nth-child(7), .iconStyle2 .box:nth-child(7)  { grid-area: 6 / 3 / 7 / 5; }
.tasksCalendar[view='week'].style3 .grid, .iconStyle3 { grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr 1fr; grid-template-columns: 1fr; }
.tasksCalendar[view='week'].style4 .grid, .iconStyle4 { grid-template-rows: 1fr; grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr; }
.tasksCalendar[view='week'].style5 .grid, .iconStyle5 { grid-template-columns: repeat(2, 1fr); grid-template-rows: repeat(10, 1fr); }
.tasksCalendar[view='week'].style5 .grid .cell:nth-child(1), .iconStyle5 .box:nth-child(1) { grid-area: 1 / 1 / 3 / 2; }
.tasksCalendar[view='week'].style5 .grid .cell:nth-child(2), .iconStyle5 .box:nth-child(2) { grid-area: 3 / 1 / 5 / 2; }
.tasksCalendar[view='week'].style5 .grid .cell:nth-child(3), .iconStyle5 .box:nth-child(3) { grid-area: 5 / 1 / 7 / 2; }
.tasksCalendar[view='week'].style5 .grid .cell:nth-child(4), .iconStyle5 .box:nth-child(4) { grid-area: 7 / 1 / 9 / 2; }
.tasksCalendar[view='week'].style5 .grid .cell:nth-child(5), .iconStyle5 .box:nth-child(5) { grid-area: 9 / 1 / 11 / 2; }
.tasksCalendar[view='week'].style5 .grid .cell:nth-child(6), .iconStyle5 .box:nth-child(6) { grid-area: 1 / 2 / 6 / 3; }
.tasksCalendar[view='week'].style5 .grid .cell:nth-child(7), .iconStyle5 .box:nth-child(7) { grid-area: 6 / 2 / 11 / 3; }
.tasksCalendar[view='week'].style6 .grid, .iconStyle6 { grid-template-columns: repeat(3, 1fr); grid-template-rows: repeat(10, 1fr); }
.tasksCalendar[view='week'].style6 .grid .cell:nth-child(1), .iconStyle6 .box:nth-child(1) { grid-area: 1 / 1 / 3 / 3; }
.tasksCalendar[view='week'].style6 .grid .cell:nth-child(2), .iconStyle6 .box:nth-child(2) { grid-area: 3 / 1 / 5 / 3; }
.tasksCalendar[view='week'].style6 .grid .cell:nth-child(3), .iconStyle6 .box:nth-child(3) { grid-area: 5 / 1 / 7 / 3; }
.tasksCalendar[view='week'].style6 .grid .cell:nth-child(4), .iconStyle6 .box:nth-child(4) { grid-area: 7 / 1 / 9 / 3; }
.tasksCalendar[view='week'].style6 .grid .cell:nth-child(5), .iconStyle6 .box:nth-child(5) { grid-area: 9 / 1 / 11 / 3; }
.tasksCalendar[view='week'].style6 .grid .cell:nth-child(6), .iconStyle6 .box:nth-child(6) { grid-area: 1 / 3 / 6 / 4; }
.tasksCalendar[view='week'].style6 .grid .cell:nth-child(7), .iconStyle6 .box:nth-child(7) { grid-area: 6 / 3 / 11 / 4; }
.tasksCalendar[view='week'].style7 .grid, .iconStyle7 { grid-template-columns: repeat(2, 1fr); grid-template-rows: repeat(8, 1fr); }
.tasksCalendar[view='week'].style7 .grid .cell:nth-child(1), .iconStyle7 .box:nth-child(1) { grid-area: 1 / 1 / 3 / 2; }
.tasksCalendar[view='week'].style7 .grid .cell:nth-child(2), .iconStyle7 .box:nth-child(2) { grid-area: 3 / 1 / 5 / 2; }
.tasksCalendar[view='week'].style7 .grid .cell:nth-child(3), .iconStyle7 .box:nth-child(3) { grid-area: 5 / 1 / 7 / 2; }
.tasksCalendar[view='week'].style7 .grid .cell:nth-child(4), .iconStyle7 .box:nth-child(4) { grid-area: 7 / 1 / 9 / 2; }
.tasksCalendar[view='week'].style7 .grid .cell:nth-child(5), .iconStyle7 .box:nth-child(5) { grid-area: 1 / 2 / 3 / 3; } 
.tasksCalendar[view='week'].style7 .grid .cell:nth-child(6), .iconStyle7 .box:nth-child(6) { grid-area: 3 / 2 / 6 / 3; } 
.tasksCalendar[view='week'].style7 .grid .cell:nth-child(7), .iconStyle7 .box:nth-child(7) { grid-area: 6 / 2 / 9 / 3; } 
.tasksCalendar[view='week'].style8 .grid, .iconStyle8 { grid-template-columns: repeat(3, 1fr); grid-template-rows: repeat(5, 1fr); }
.tasksCalendar[view='week'].style8 .grid .cell:nth-child(1), .iconStyle8 .box:nth-child(1) { grid-area: 1 / 1 / 3 / 2; }
.tasksCalendar[view='week'].style8 .grid .cell:nth-child(2), .iconStyle8 .box:nth-child(2) { grid-area: 1 / 2 / 3 / 3; }
.tasksCalendar[view='week'].style8 .grid .cell:nth-child(3), .iconStyle8 .box:nth-child(3) { grid-area: 1 / 3 / 3 / 4; }
.tasksCalendar[view='week'].style8 .grid .cell:nth-child(4), .iconStyle8 .box:nth-child(4) { grid-area: 3 / 1 / 5 / 2; }
.tasksCalendar[view='week'].style8 .grid .cell:nth-child(5), .iconStyle8 .box:nth-child(5) { grid-area: 3 / 2 / 5 / 3; }
.tasksCalendar[view='week'].style8 .grid .cell:nth-child(6), .iconStyle8 .box:nth-child(6) { grid-area: 3 / 3 / 5 / 4; }
.tasksCalendar[view='week'].style8 .grid .cell:nth-child(7), .iconStyle8 .box:nth-child(7) { grid-area: 5 / 1 / 6 / 4; }
.tasksCalendar[view='week'].style9 .grid, .iconStyle9 { grid-template-columns: repeat(10, 1fr); grid-template-rows: repeat(3, 1fr); }
.tasksCalendar[view='week'].style9 .grid .cell:nth-child(1), .iconStyle9 .box:nth-child(1) { grid-area: 1 / 1 / 3 / 3; } 
.tasksCalendar[view='week'].style9 .grid .cell:nth-child(2), .iconStyle9 .box:nth-child(2) { grid-area: 1 / 3 / 3 / 5; } 
.tasksCalendar[view='week'].style9 .grid .cell:nth-child(3), .iconStyle9 .box:nth-child(3) { grid-area: 1 / 5 / 3 / 7; } 
.tasksCalendar[view='week'].style9 .grid .cell:nth-child(4), .iconStyle9 .box:nth-child(4) { grid-area: 1 / 7 / 3 / 9; } 
.tasksCalendar[view='week'].style9 .grid .cell:nth-child(5), .iconStyle9 .box:nth-child(5) { grid-area: 1 / 9 / 3 / 11; } 
.tasksCalendar[view='week'].style9 .grid .cell:nth-child(6), .iconStyle9 .box:nth-child(6) { grid-area: 3 / 1 / 4 / 6; } 
.tasksCalendar[view='week'].style9 .grid .cell:nth-child(7), .iconStyle9 .box:nth-child(7) { grid-area: 3 / 6 / 4 / 11; } 
.tasksCalendar[view='week'].style10 .grid, .iconStyle10 { grid-template-columns: repeat(10, 1fr); grid-template-rows: repeat(3, 1fr); }
.tasksCalendar[view='week'].style10 .grid .cell:nth-child(1), .iconStyle10 .box:nth-child(1) { grid-area: 1 / 1 / 4 / 3; } 
.tasksCalendar[view='week'].style10 .grid .cell:nth-child(2), .iconStyle10 .box:nth-child(2) { grid-area: 1 / 3 / 4 / 5; } 
.tasksCalendar[view='week'].style10 .grid .cell:nth-child(3), .iconStyle10 .box:nth-child(3) { grid-area: 1 / 5 / 4 / 7; } 
.tasksCalendar[view='week'].style10 .grid .cell:nth-child(4), .iconStyle10 .box:nth-child(4) { grid-area: 1 / 7 / 3 / 9; } 
.tasksCalendar[view='week'].style10 .grid .cell:nth-child(5), .iconStyle10 .box:nth-child(5) { grid-area: 1 / 9 / 3 / 11; } 
.tasksCalendar[view='week'].style10 .grid .cell:nth-child(6), .iconStyle10 .box:nth-child(6) { grid-area: 3 / 7 / 4 / 9; } 
.tasksCalendar[view='week'].style10 .grid .cell:nth-child(7), .iconStyle10 .box:nth-child(7) { grid-area: 3 / 9 / 4 / 11; } 
.tasksCalendar[view='week'].style11 .grid, .iconStyle11 { grid-template-rows: 1fr; grid-template-columns: 1fr 1fr 1fr 1fr 1fr; }
.tasksCalendar[view='week'].style11 .grid { height: 300px }
.tasksCalendar[view='week'].style11 .cell[data-weekday="0"], .iconStyle11 { display: none !important }
.tasksCalendar[view='week'].style11 .cell[data-weekday="6"], .iconStyle11 { display: none !important }

/* Options classes */
.tasksCalendar.noIcons .task .icon { display: none !important; }
.tasksCalendar:not(.noFilename) .task.noNoteIcon .icon { display: none !important; }
.tasksCalendar.noFilename .task .note { display: none !important; }
.tasksCalendar.filter .task.done, .tasksCalendar.filter .task.cancelled { display: none !important; }
.tasksCalendar.filter #statisticDone { pointer-events: none !important; color: var(--text-faint) !important; }
.tasksCalendar.noScheduled .task.scheduled { display: none !important; }
.tasksCalendar.noStart .task.start { display: none !important; }
.tasksCalendar.noDue .task.due { display: none !important; }
.tasksCalendar.noDone .task.done { display: none !important; }
.tasksCalendar.noProcess .task.process { display: none !important; }
.tasksCalendar.noRecurrence .task.recurrence { display: none !important; }
.tasksCalendar.noOverdue .task.overdue { display: none !important; }
.tasksCalendar.noDailyNote .task.dailyNote { display: none !important; }
.tasksCalendar.noCellNameEvent .cellName { pointer-events: none !important; }
.tasksCalendar.noLayer .grid .wrappers:before,
.tasksCalendar.noLayer .grid:before,
.tasksCalendar.noLayer .list:before { display: none !important;}
.tasksCalendar.focusDone .task { opacity: 0.25 !important; }
.tasksCalendar.focusDone .task.done { opacity: 1 !important; }
.tasksCalendar.focusDue .task { opacity: 0.25 !important; }
.tasksCalendar.focusDue .task.due { opacity: 1 !important; }
.tasksCalendar.focusOverdue .task { opacity: 0.25 !important; }
.tasksCalendar.focusOverdue .task.overdue { opacity: 1 !important; }
.tasksCalendar.focusStart .task { opacity: 0.25 !important; }
.tasksCalendar.focusStart .task.start { opacity: 1 !important; }
.tasksCalendar.focusScheduled .task { opacity: 0.25 !important; }
.tasksCalendar.focusScheduled .task.scheduled { opacity: 1 !important; }
.tasksCalendar.focusRecurrence .task { opacity: 0.25 !important; }
.tasksCalendar.focusRecurrence .task.recurrence { opacity: 1 !important; }
.tasksCalendar.focusDailyNote .task { opacity: 0.25 !important; }
.tasksCalendar.focusDailyNote .task.dailyNote { opacity: 1 !important; }
.tasksCalendar.mini { max-width: 500px !important; margin: 0 auto; }
.tasksCalendar.mini .grid { height: 400px !important; }
.tasksCalendar.mini .gridHead,
.tasksCalendar.mini .cellName,
.tasksCalendar.mini .task,
.tasksCalendar.mini .wrapperButton { font-size: 9px !important; }
.tasksCalendar.mini .wrappers:before,
.tasksCalendar.mini .grid:before { font-size: 70px !important; }
.tasksCalendar.mini .statisticPopup li,
.tasksCalendar.mini .weekViewContext li { font-size: 9px !important; }
.tasksCalendar.noWeekNr .wrapperButton { visibility: hidden !important; width: 0 !important; }
.tasksCalendar.noWeekNr .gridHead:first-child { visibility: hidden !important; width: 0 !important; }
.tasksCalendar.noWeekNr .wrapper { grid-template-columns: 0px 1fr 1fr 1fr 1fr 1fr 1fr 1fr !important; }
.tasksCalendar.noWeekNr .gridHeads { grid-template-columns: 0px 1fr 1fr 1fr 1fr 1fr 1fr 1fr !important; }
.tasksCalendar.noWeekNr .list .weekNr { display: none !important; }
.tasksCalendar.lineClamp1 .task .inner { -webkit-line-clamp: 1 !important; white-space: nowrap !important; }
.tasksCalendar.lineClamp2 .task .inner { -webkit-line-clamp: 2 !important; }
.tasksCalendar.lineClamp3 .task .inner { -webkit-line-clamp: 3 !important; }
.tasksCalendar.noLineClamp .task .inner { display: block !important; }
.tasksCalendar.noOverdueFlag .task .description:before { display: none !important; }

/* Mobile View */
body.is-mobile .tasksCalendar .gridHead, body.is-mobile .tasksCalendar .cellName, body.is-mobile .tasksCalendar .task { font-size: 9px; }
body.is-mobile .tasksCalendar[view='week']:not(.style4) .cellName,
body.is-mobile .tasksCalendar[view='week']:not(.style4) .task { font-size: 13px !important; }
body.is-mobile .tasksCalendar .statisticPopup li { font-size: 13px !important; }

/*# sourceURL=app://obsidian.md/3_Archive/ETCs/tasksCalendar/view.css */</style><div class="tasksCalendar style1 noDone noCellNameEvent noFilename noLineClamp noLayer noIcons mini" id="tasksCalendar1722011098072" view="month" style="position:relative;-webkit-user-select:none!important"><span><div class="buttons"><span><button class="filter"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><polygon points="22 3 2 3 10 12.46 10 19 14 21 14 12.46 22 3"></polygon></svg></button><button title="List" class="listView"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><line y2="6" x2="21" y1="6" x1="8"></line><line y2="12" x2="21" y1="12" x1="8"></line><line y2="18" x2="21" y1="18" x1="8"></line><line y2="6" x2="3.01" y1="6" x1="3"></line><line y2="12" x2="3.01" y1="12" x1="3"></line><line y2="18" x2="3.01" y1="18" x1="3"></line></svg></button><button title="Month" class="monthView"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><rect ry="2" rx="2" height="18" width="18" y="4" x="3"></rect><line y2="6" x2="16" y1="2" x1="16"></line><line y2="6" x2="8" y1="2" x1="8"></line><line y2="10" x2="21" y1="10" x1="3"></line><path d="M8 14h.01"></path><path d="M12 14h.01"></path><path d="M16 14h.01"></path><path d="M8 18h.01"></path><path d="M12 18h.01"></path><path d="M16 18h.01"></path></svg></button><button title="Week" class="weekView"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><rect ry="2" rx="2" height="18" width="18" y="4" x="3"></rect><line y2="6" x2="16" y1="2" x1="16"></line><line y2="6" x2="8" y1="2" x1="8"></line><line y2="10" x2="21" y1="10" x1="3"></line><path d="M17 14h-6"></path><path d="M13 18H7"></path><path d="M7 14h.01"></path><path d="M17 18h.01"></path></svg></button><button class="current"><span>July</span><span> 2024</span></button><button class="previous"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><line y2="12" x2="5" y1="12" x1="19"></line><polyline points="12 19 5 12 12 5"></polyline></svg></button><button class="next"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><line y2="12" x2="19" y1="12" x1="5"></line><polyline points="12 5 19 12 12 19"></polyline></svg></button><button class="statistic" data-percentage="53" data-remaining="8"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 7.5V6a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h3.5"></path><path d="M16 2v4"></path><path d="M8 2v4"></path><path d="M3 10h5"></path><path d="M17.5 17.5 16 16.25V14"></path><path d="M22 16a6 6 0 1 1-12 0 6 6 0 0 1 12 0Z"></path></svg></button></span></div><ul class="statisticPopup"><span><li data-group="done" id="statisticDone" dir="auto">✅ Done: 9/17</li><li data-group="due" id="statisticDue" dir="auto">📅 Due: 8</li><li data-group="overdue" id="statisticOverdue" dir="auto">⚠️ Overdue: 0</li><li class="break" dir="auto"></li><li data-group="start" id="statisticStart" dir="auto">🛫 Start: 0</li><li data-group="scheduled" id="statisticScheduled" dir="auto">⏳ Scheduled: 5</li><li data-group="recurrence" id="statisticRecurrence" dir="auto">🔁 Recurrence: 0</li><li class="break" dir="auto"></li><li data-group="dailyNote" id="statisticDailyNote" dir="auto">📄 Daily Notes: 3</li></span></ul><ul class="weekViewContext"><span><li data-style="style1" dir="auto" class="active"><div class="liIcon iconStyle1"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 1</li><li data-style="style2" dir="auto"><div class="liIcon iconStyle2"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 2</li><li data-style="style3" dir="auto"><div class="liIcon iconStyle3"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 3</li><li data-style="style4" dir="auto"><div class="liIcon iconStyle4"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 4</li><li data-style="style5" dir="auto"><div class="liIcon iconStyle5"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 5</li><li data-style="style6" dir="auto"><div class="liIcon iconStyle6"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 6</li><li data-style="style7" dir="auto"><div class="liIcon iconStyle7"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 7</li><li data-style="style8" dir="auto"><div class="liIcon iconStyle8"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 8</li><li data-style="style9" dir="auto"><div class="liIcon iconStyle9"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 9</li><li data-style="style10" dir="auto"><div class="liIcon iconStyle10"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 10</li><li data-style="style11" dir="auto"><div class="liIcon iconStyle11"><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div><div class="box"></div></div>Style 11</li></span></ul><div class="grid"><span><div class="gridHeads"><div class="gridHead"></div><div data-weekday="0" class="gridHead">Sun</div><div data-weekday="1" class="gridHead">Mon</div><div data-weekday="2" class="gridHead">Tue</div><div data-weekday="3" class="gridHead">Wed</div><div data-weekday="4" class="gridHead">Thu</div><div data-weekday="5" class="gridHead">Fri</div><div data-weekday="6" class="gridHead today">Sat</div></div><div data-month="Jul" class="wrappers"><div class="wrapper"><div data-year="2024" data-week="27" class="wrapperButton">W27</div><div data-weekday="0" class="cell prevMonth"><a href="3_Archive/32_Daily Notes/2024-06-30" class="internal-link cellName" target="_blank" rel="noopener">30</a><div class="cellContent"></div></div><div data-weekday="1" class="cell currentMonth newMonth"><a href="3_Archive/32_Daily Notes/2024-07-01" class="internal-link cellName" target="_blank" rel="noopener">1. Jul</a><div class="cellContent"></div></div><div data-weekday="2" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-02" class="internal-link cellName" target="_blank" rel="noopener">2</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-06-25.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-06-25:   Vision to PCD 🔺" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-06-25</div><div class="icon">✅</div><div data-relative="a month ago" class="description">  Vision to PCD 🔺 </div></div></div></a></div></div><div data-weekday="3" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-03" class="internal-link cellName" target="_blank" rel="noopener">3</a><div class="cellContent"></div></div><div data-weekday="4" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-04" class="internal-link cellName" target="_blank" rel="noopener">4</a><div class="cellContent"></div></div><div data-weekday="5" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-05" class="internal-link cellName" target="_blank" rel="noopener">5</a><div class="cellContent"></div></div><div data-weekday="6" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-06" class="internal-link cellName" target="_blank" rel="noopener">6</a><div class="cellContent"></div></div></div><div class="wrapper"><div data-year="2024" data-week="28" class="wrapperButton">W28</div><div data-weekday="0" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-07" class="internal-link cellName" target="_blank" rel="noopener">7</a><div class="cellContent"></div></div><div data-weekday="1" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-08" class="internal-link cellName" target="_blank" rel="noopener">8</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-05.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-07-05:  월세 자동이체" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-07-05</div><div class="icon">✅</div><div data-relative="" class="description"> 월세 자동이체 </div></div></div></a><a href="3_Archive/32_Daily Notes/2024-07-05.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-07-05:  이발 예약 #03" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-07-05</div><div class="icon">✅</div><div data-relative="21 days ago" class="description"> 이발 예약 #03  </div></div></div></a></div></div><div data-weekday="2" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-09" class="internal-link cellName" target="_blank" rel="noopener">9</a><div class="cellContent"></div></div><div data-weekday="3" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-10" class="internal-link cellName" target="_blank" rel="noopener">10</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-10.md" class="internal-link" target="_blank" rel="noopener"><div title="📄&nbsp;2024-07-10:  Docker 끼리 ROS 통신 #Tags/0c70f2/Study" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task dailyNote noNoteIcon"><div class="inner"><div class="note">📄&nbsp;2024-07-10</div><div class="icon">📄</div><div data-relative="" class="description"> Docker 끼리 ROS 통신 #Tags/0c70f2/Study</div></div></div></a></div></div><div data-weekday="4" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-11" class="internal-link cellName" target="_blank" rel="noopener">11</a><div class="cellContent"></div></div><div data-weekday="5" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-12" class="internal-link cellName" target="_blank" rel="noopener">12</a><div class="cellContent"></div></div><div data-weekday="6" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-13" class="internal-link cellName" target="_blank" rel="noopener">13</a><div class="cellContent"></div></div></div><div class="wrapper"><div data-year="2024" data-week="29" class="wrapperButton">W29</div><div data-weekday="0" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-14" class="internal-link cellName" target="_blank" rel="noopener">14</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-08.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-07-08:  Reconstruction from Stereo with ROS" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-07-08</div><div class="icon">✅</div><div data-relative="" class="description"> Reconstruction from Stereo with ROS  </div></div></div></a></div></div><div data-weekday="1" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-15" class="internal-link cellName" target="_blank" rel="noopener">15</a><div class="cellContent"></div></div><div data-weekday="2" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-16" class="internal-link cellName" target="_blank" rel="noopener">16</a><div class="cellContent"></div></div><div data-weekday="3" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-17" class="internal-link cellName" target="_blank" rel="noopener">17</a><div class="cellContent"></div></div><div data-weekday="4" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-18" class="internal-link cellName" target="_blank" rel="noopener">18</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-05.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-07-05:  휴대폰 요금 변경" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-07-05</div><div class="icon">✅</div><div data-relative="" class="description"> 휴대폰 요금 변경  </div></div></div></a></div></div><div data-weekday="5" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-19" class="internal-link cellName" target="_blank" rel="noopener">19</a><div class="cellContent"></div></div><div data-weekday="6" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-20" class="internal-link cellName" target="_blank" rel="noopener">20</a><div class="cellContent"></div></div></div><div class="wrapper"><div data-year="2024" data-week="30" class="wrapperButton">W30</div><div data-weekday="0" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-21" class="internal-link cellName" target="_blank" rel="noopener">21</a><div class="cellContent"></div></div><div data-weekday="1" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-22" class="internal-link cellName" target="_blank" rel="noopener">22</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-22.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-07-22:  옵시디언 정리 #Tags/ff443a/HERO 🔺" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-07-22</div><div class="icon">✅</div><div data-relative="" class="description"> 옵시디언 정리 #Tags/ff443a/HERO 🔺  </div></div></div></a><a href="3_Archive/32_Daily Notes/2024-07-22.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-07-22:  옵시디언 퍼블리시 및 휴대폰 #Tags/a374db/ETCs/Obsidian" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-07-22</div><div class="icon">✅</div><div data-relative="" class="description"> 옵시디언 퍼블리시 및 휴대폰 #Tags/a374db/ETCs/Obsidian  </div></div></div></a></div></div><div data-weekday="2" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-23" class="internal-link cellName" target="_blank" rel="noopener">23</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-23.md" class="internal-link" target="_blank" rel="noopener"><div title="📄&nbsp;2024-07-23:  다이소 접이형 박스 3개 #Tags/ffe880/Shopping" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task dailyNote noNoteIcon"><div class="inner"><div class="note">📄&nbsp;2024-07-23</div><div class="icon">📄</div><div data-relative="" class="description"> 다이소 접이형 박스 3개 #Tags/ffe880/Shopping</div></div></div></a></div></div><div data-weekday="3" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-24" class="internal-link cellName" target="_blank" rel="noopener">24</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-11.md" class="internal-link" target="_blank" rel="noopener"><div title="⏳&nbsp;2024-07-11:  입학 통지서 자세히 확인  ⏫ #Tags/a374db/ETCs" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task scheduled noNoteIcon"><div class="inner"><div class="note">⏳&nbsp;2024-07-11</div><div class="icon">⏳</div><div data-relative="" class="description"> 입학 통지서 자세히 확인  ⏫ #Tags/a374db/ETCs</div></div></div></a><a href="3_Archive/32_Daily Notes/2024-07-18.md" class="internal-link" target="_blank" rel="noopener"><div title="⏳&nbsp;2024-07-18:  장학금 확인  #Tags/a374db/ETCs" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task scheduled noNoteIcon"><div class="inner"><div class="note">⏳&nbsp;2024-07-18</div><div class="icon">⏳</div><div data-relative="" class="description"> 장학금 확인  #Tags/a374db/ETCs</div></div></div></a><a href="3_Archive/32_Daily Notes/2024-07-24.md" class="internal-link" target="_blank" rel="noopener"><div title="📄&nbsp;2024-07-24:  금도 시스템 견적서 정리 #Tags/ff443a/HERO" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task dailyNote noNoteIcon"><div class="inner"><div class="note">📄&nbsp;2024-07-24</div><div class="icon">📄</div><div data-relative="" class="description"> 금도 시스템 견적서 정리 #Tags/ff443a/HERO</div></div></div></a><a href="3_Archive/32_Daily Notes/2024-07-22.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-07-22:  실험 도구들 정리 #Tags/ff443a/HERO ⏫" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-07-22</div><div class="icon">✅</div><div data-relative="" class="description"> 실험 도구들 정리 #Tags/ff443a/HERO ⏫  </div></div></div></a><a href="3_Archive/32_Daily Notes/2024-07-24.md" class="internal-link" target="_blank" rel="noopener"><div title="✅&nbsp;2024-07-24:  인턴 기간 연장 확인 #Tags/ff443a/HERO 🔺" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task done noNoteIcon"><div class="inner"><div class="note">✅&nbsp;2024-07-24</div><div class="icon">✅</div><div data-relative="" class="description"> 인턴 기간 연장 확인 #Tags/ff443a/HERO 🔺  </div></div></div></a></div></div><div data-weekday="4" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-25" class="internal-link cellName" target="_blank" rel="noopener">25</a><div class="cellContent"></div></div><div data-weekday="5" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-26" class="internal-link cellName" target="_blank" rel="noopener">26</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-24.md" class="internal-link" target="_blank" rel="noopener"><div title="⏳&nbsp;2024-07-24:  3D 프린터 구매요청서 마무리 후 건우 선배님께 전달  🔺 #Tags/ff443a/HERO" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task scheduled noNoteIcon"><div class="inner"><div class="note">⏳&nbsp;2024-07-24</div><div class="icon">⏳</div><div data-relative="" class="description"> 3D 프린터 구매요청서 마무리 후 건우 선배님께 전달  🔺 #Tags/ff443a/HERO</div></div></div></a></div></div><div data-weekday="6" class="cell currentMonth today"><a href="3_Archive/32_Daily Notes/2024-07-27" class="internal-link cellName" target="_blank" rel="noopener">27</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-26.md" class="internal-link" target="_blank" rel="noopener"><div title="⏳&nbsp;2024-07-26:  거미 몸통 위에서 아래로 관통하는 나사 추가" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task scheduled noNoteIcon"><div class="inner"><div class="note">⏳&nbsp;2024-07-26</div><div class="icon">⏳</div><div data-relative="" class="description"> 거미 몸통 위에서 아래로 관통하는 나사 추가 </div></div></div></a><a href="3_Archive/32_Daily Notes/2024-07-26.md" class="internal-link" target="_blank" rel="noopener"><div title="⏳&nbsp;2024-07-26:  나인봇 전기테이프" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task scheduled noNoteIcon"><div class="inner"><div class="note">⏳&nbsp;2024-07-26</div><div class="icon">⏳</div><div data-relative="" class="description"> 나인봇 전기테이프</div></div></div></a></div></div></div><div class="wrapper"><div data-year="2024" data-week="31" class="wrapperButton">W31</div><div data-weekday="0" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-28" class="internal-link cellName" target="_blank" rel="noopener">28</a><div class="cellContent"></div></div><div data-weekday="1" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-29" class="internal-link cellName" target="_blank" rel="noopener">29</a><div class="cellContent"></div></div><div data-weekday="2" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-30" class="internal-link cellName" target="_blank" rel="noopener">30</a><div class="cellContent"></div></div><div data-weekday="3" class="cell currentMonth"><a href="3_Archive/32_Daily Notes/2024-07-31" class="internal-link cellName" target="_blank" rel="noopener">31</a><div class="cellContent"></div></div><div data-weekday="4" class="cell nextMonth newMonth"><a href="3_Archive/32_Daily Notes/2024-08-01" class="internal-link cellName" target="_blank" rel="noopener">1. Aug</a><div class="cellContent"></div></div><div data-weekday="5" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-02" class="internal-link cellName" target="_blank" rel="noopener">2</a><div class="cellContent"></div></div><div data-weekday="6" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-03" class="internal-link cellName" target="_blank" rel="noopener">3</a><div class="cellContent"></div></div></div><div class="wrapper"><div data-year="2024" data-week="32" class="wrapperButton">W32</div><div data-weekday="0" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-04" class="internal-link cellName" target="_blank" rel="noopener">4</a><div class="cellContent"></div></div><div data-weekday="1" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-05" class="internal-link cellName" target="_blank" rel="noopener">5</a><div class="cellContent"></div></div><div data-weekday="2" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-06" class="internal-link cellName" target="_blank" rel="noopener">6</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-06-10.md" class="internal-link" target="_blank" rel="noopener"><div title="🛫&nbsp;2024-06-10:  💸포항공대 등록금 납부   ⏫ #Tags/a374db/ETCs" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task start noNoteIcon"><div class="inner"><div class="note">🛫&nbsp;2024-06-10</div><div class="icon">🛫</div><div data-relative="in 12 days" class="description"> 💸포항공대 등록금 납부   ⏫ #Tags/a374db/ETCs</div></div></div></a></div></div><div data-weekday="3" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-07" class="internal-link cellName" target="_blank" rel="noopener">7</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-06-10.md" class="internal-link" target="_blank" rel="noopener"><div title="⏺️&nbsp;2024-06-10:  💸포항공대 등록금 납부   ⏫ #Tags/a374db/ETCs" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task process noNoteIcon"><div class="inner"><div class="note">⏺️&nbsp;2024-06-10</div><div class="icon">⏺️</div><div data-relative="in 12 days" class="description"> 💸포항공대 등록금 납부   ⏫ #Tags/a374db/ETCs</div></div></div></a></div></div><div data-weekday="4" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-08" class="internal-link cellName" target="_blank" rel="noopener">8</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-06-10.md" class="internal-link" target="_blank" rel="noopener"><div title="📅&nbsp;2024-06-10:  💸포항공대 등록금 납부   ⏫ #Tags/a374db/ETCs" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task due noNoteIcon"><div class="inner"><div class="note">📅&nbsp;2024-06-10</div><div class="icon">📅</div><div data-relative="in 12 days" class="description"> 💸포항공대 등록금 납부   ⏫ #Tags/a374db/ETCs</div></div></div></a></div></div><div data-weekday="5" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-09" class="internal-link cellName" target="_blank" rel="noopener">9</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-11.md" class="internal-link" target="_blank" rel="noopener"><div title="🛫&nbsp;2024-07-11:  해양 박람회   #Tags/ff443a/HERO" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task start noNoteIcon"><div class="inner"><div class="note">🛫&nbsp;2024-07-11</div><div class="icon">🛫</div><div data-relative="in 16 days" class="description"> 해양 박람회   #Tags/ff443a/HERO</div></div></div></a></div></div><div data-weekday="6" class="cell nextMonth"><a href="3_Archive/32_Daily Notes/2024-08-10" class="internal-link cellName" target="_blank" rel="noopener">10</a><div class="cellContent"><a href="3_Archive/32_Daily Notes/2024-07-11.md" class="internal-link" target="_blank" rel="noopener"><div title="⏺️&nbsp;2024-07-11:  해양 박람회   #Tags/ff443a/HERO" style="--task-background:#7D7D7D33;--task-color:#7D7D7D;--dark-task-text-color:#171717;--light-task-text-color:#bdbdbd" class="task process noNoteIcon"><div class="inner"><div class="note">⏺️&nbsp;2024-07-11</div><div class="icon">⏺️</div><div data-relative="in 16 days" class="description"> 해양 박람회   #Tags/ff443a/HERO</div></div></div></a></div></div></div></div></span></div></span></div>

<style scope=" ">.taskido {
	cursor: default;
	user-select: none;
}
.taskido a {
	text-decoration: none !important;
	color: inherit !important;
}
.taskido span {
	display: contents;
}
.taskido .task .innerLink,
.taskido .task .outerLink {
	color: var(--interactive-accent);
	text-decoration: underline !important;
}
.taskido .year {
	font-size: 30px;
	font-weight: bold;
	margin: 20px 0;
	color: var(--text-normal);
	text-align: center;
}
.taskido .details {
	display: flex;
	flex-direction: column;
	flex-wrap: nowrap;
	width: 100%;
	height: auto;
}
.taskido .todayHeader {
	font-size: 24px;
	font-weight: bold;
	text-align: center;
	margin: 10px 5px;
	border-radius: 10px;
	cursor: pointer;
}
.taskido .details.today {
	padding: 30px 0;
}
.taskido .counters {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: center;
	align-content: center;
	margin: 20px 0;
}
.taskido .counter {
	display: flex;
	flex-direction: column;
	flex-wrap: nowrap;
	color: var(--text-normal);
	border-radius: 10px;
	padding: 5px;
	text-align: center;
	flex: 1 1 0;
	margin: 0 5px;
	min-width: 70px;
	max-width: 150px;
	overflow: hidden;
	background: var(--interactive-normal);
	box-shadow: var(--input-shadow);
	cursor: pointer;
}
.taskido .count {
	font-size: 18px;
	font-weight: normal;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.taskido .counter .label {
	font-size: 12px;
	font-weight: normal;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.taskido .dateLine {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: space-between;
	align-items: center;
	margin: 10px 0;
}
.taskido .date {
	color: var(--text-normal);
	font-size: 16px;
	font-weight: bold;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.taskido .weekday {
	color: var(--text-normal);
	font-weight: normal;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
	font-size: 16px;
}
.taskido .task {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	border-radius: 10px;
	padding: 0;
	margin: 0;
	cursor: pointer;
}
.taskido .timeline,
.taskido .lines {
	display: flex;
	flex-direction: column;
	flex-wrap: nowrap;
	cursor: default;
}
.taskido .timeline {
	width: 50px;
	flex-shrink: 0;
	flex-grow: 0;
}
.taskido .lines {
	flex-shrink: 1;
	flex-grow: 1;
	overflow: hidden;
}
.taskido .stripe {
	display: flex;
	justify-content: center;
	align-items: center;
	flex-shrink: 1;
	flex-grow: 1;
	margin: 0 auto;
	width: 1px;
	background: var(--checkbox-border-color);
}
.taskido .task.overdue .timeline .icon svg line {
	stroke: #ff375f !important;
	stroke-width: 2.5px !important;
}
.taskido .task.done .timeline .icon svg {
	fill: var(--interactive-accent) !important;
	stroke: var(--interactive-accent) !important;
}
.taskido .task.done .timeline .icon svg path:nth-child(1) {
	fill: var(--interactive-accent) !important;
}
.taskido .task.done .timeline .icon svg path:nth-child(2) {
	stroke: var(--checkbox-marker-color) !important;
	stroke-width: 2.5px;
}
.taskido .task.done .info .tag,
.taskido .task.done .info .repeat,
.taskido .task.done .info .priority,
.taskido .task.done .info .relative,
.taskido .task.done .info .file,
.taskido .task.cancelled .info .tag,
.taskido .task.cancelled .info .repeat,
.taskido .task.cancelled .info .priority,
.taskido .task.cancelled .info .relative,
.taskido .task.cancelled .info .file {
	color: var(--text-muted) !important;
	line-height: 0;
}
.taskido .task.done .content,
.taskido .task.cancelled .content {
	text-decoration: line-through;
	color: var(--text-muted);
}
.taskido .line {
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	align-items: center;
}
.taskido .icon {
	display: flex;
	justify-content: center;
	align-items: center;
	flex-shrink: 0;
	flex-grow: 0;
	text-align: center;
}
.taskido .timeline .icon {
	text-align: center;
	height: 22px;
}
.taskido .timeline .icon svg {
	color: var(--checkbox-border-color);
}
.taskido .timeline .icon svg:hover {
	color: var(--checkbox-border-color-hover);
}
.taskido .timeline .icon svg {
	height: var(--checkbox-size);
	width: var(--checkbox-size);
	stroke-width: 1.75px;
}
.taskido .task .info {
	line-height: 22px;
	padding-bottom: 2px;
	cursor: default;
}
.taskido .task .info:empty {
	display: none;
}
.taskido .task .content {
	display: block;
	white-space: break-word;
	font-size: 15px;
	font-weight: normal;
	color: var(--text-normal);
	line-height: 22px;
}
.taskido .task .info .tag,
.taskido .task .info .repeat,
.taskido .task .info .priority,
.taskido .task .info .relative,
.taskido .task .info .file {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	align-items: center;
	width: auto;
	font-size: 9px;
	font-weight: normal;
	margin: 2px 5px 2px 0;
	color: var(--text-muted);
	padding: 0px;
	border: none;
	line-height: 1 !important;
	padding: 0;
	border-radius: 3px !important;
}
.taskido .task .info .file {
	color: var(--task-color);
}
.taskido .task .info .tag {
	color: var(--tag-color) !important;
	background: none !important;
	cursor: pointer;
}
.taskido .info .icon {
	text-align: center;
	height: 15px;
}
.taskido .info .label {
	margin-left: 2px;
}
.taskido .info svg {
	height: 12px;
	width: 12px;
	stroke-width: 1.75px;
}
.taskido .task.overdue .info .relative {
	color: #ff375f !important;
}
/* Quick Entry Panel */
.taskido .quickEntryPanel {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	background: var(--background-modifier-form-field);
	border: var(--input-border-width) solid var(--background-modifier-border);
	color: var(--text-normal);
	border-radius: 10px;
	box-shadow: 0 0 5px 0 rgba(0,0,0,0.1);
	margin: 0 5px 20px 5px;
	overflow: hidden;
	padding: 5px;
}
.taskido .quickEntryPanel .left {
	display: flex;
	flex-direction: column;
	flex-wrap: nowrap;
	align-items: center;
	width: 100%;
	flex-shrink: 1;
	flex-grow: 1;
	overflow: hidden;
	border-radius: 5px;
	padding: 0 5px !important;
}
.taskido .quickEntryPanel .right {
	display: block;
	width: auto;
	flex-shrink: 1;
	flex-grow: 1;
	overflow: hidden;
	border-radius: 5px;
}
.taskido .quickEntryPanel select,
.taskido .quickEntryPanel input,
.taskido .quickEntryPanel button {
	box-shadow: none !important;
	border: none !important;
	background: none !important;
	border-radius: 0 !important;
}
.taskido .quickEntryPanel select,
.taskido .quickEntryPanel button {
	cursor: pointer;
}
.taskido .quickEntryPanel input {
	cursor: text;
}
.taskido .quickEntryPanel select {
	height: 15px;
	width: 100%;
	font-size: 11px;
	text-overflow: ellipsis;
	white-space: nowrap;
	overflow: hidden;
	padding: 0 !important;
	margin: 2.5px 0 !important;
	color: var(--text-muted);
}
.taskido .quickEntryPanel select:hover,
.taskido .quickEntryPanel button:hover {
	color: var(--text-normal);
}
.taskido .quickEntryPanel select option,
.taskido .quickEntryPanel select optgroup {
	background: var(--background-primary);
	font-weight: normal;
	color: var(--text-normal);
}
.taskido .quickEntryPanel input {
	height: 20px;
	line-height: 20px;
	width: 100%;
	text-overflow: ellipsis;
	white-space: nowrap;
	overflow: hidden;
	padding: 0 !important;
	margin: 0 !important;
	font-size: 14px;
}
.taskido .quickEntryPanel button {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: center;
	align-items: center;
	height: 100%;
	width: auto;
	padding: 0 5px !important;
	margin: 0 !important;
	color: var(--text-muted);
}
.taskido .quickEntryPanel svg {
	height: 15px;
	width: 15px;
	stroke-width: 1.75px;
}
.taskido .quickEntryPanel select:active,
.taskido .quickEntryPanel input:active,
.taskido .quickEntryPanel button:active {
	border: none !important;
	box-shadow: none !important;
	transition: none !important;
}
/* Classes */
.taskido.todayFocus .todayHeader {
	color: var(--interactive-accent);
}
.taskido.todoFocus .counter#todo,
.taskido.todoFilter .counter#todo,
.taskido.overdueFocus .counter#overdue,
.taskido.overdueFilter .counter#overdue,
.taskido.unplannedFocus .counter#unplanned,
.taskido.unplannedFilter .counter#unplanned { color: var(--interactive-accent); background: hsla(var(--interactive-accent-hsl), 0.2); box-shadow: var(--input-shadow); }
.taskido.noYear .year,
.taskido.noRepeat .repeat,
.taskido.noTag .tag,
.taskido.noPriority .priority,
.taskido.noFile .task .file,
.taskido.noHeader .task .header,
.taskido.noFile .task .info > .file,
.taskido.noInfo .task .line:nth-child(2),
.taskido.noDone .year[data-types="done"],
.taskido.noDone .details[data-types="done"],
.taskido.noDone .task.done,
.taskido.noUnplanned .task.unplanned,
.taskido.noUnplanned .counter#unplanned,
.taskido.noUnplanned .year[data-types="unplanned"],
.taskido.noUnplanned .details[data-types="unplanned"],
.taskido.noRelative .relative,
.taskido.noQuickEntry .quickEntryPanel,
.taskido.noCounters .counters { display: none !important; }
.taskido.noColor .task .file { color: var(--text-muted) !important }
.taskido.noColor .task .info .file { color: var(--text-muted) !important }
/* Focus */
.taskido.todayFocus .details:not(.today),
.taskido.todayFocus .year { display: none !important; }
.taskido.todayFocus .details.today { padding: 0; }
.taskido.todoFocus .details.today .task.due,
.taskido.todoFocus .details.today .task.scheduled,
.taskido.todoFocus .details.today .task.process,
.taskido.todoFocus .details.today .task.start,
.taskido.overdueFocus .task.overdue,
.taskido.unplannedFocus .task.unplanned { background: hsla(var(--interactive-accent-hsl), 0.2); }
/* Filter */
.taskido.todoFilter .year:not(.current):not([data-types*="due"][data-types*="scheduled"][data-types*="overdue"]) { display: none; }
.taskido.todoFilter .details:not(.today):not([data-types*="due"][data-types*="scheduled"][data-types*="overdue"]) { display: none; }
.taskido.todoFilter .task:not(.due, .scheduled, .process, .start) { display: none; }
.taskido.overdueFilter .year:not(.current):not([data-types*="overdue"]) { display: none; }
.taskido.overdueFilter .details:not(.today):not([data-types*="overdue"]) { display: none; }
.taskido.overdueFilter .task:not(.overdue) { display: none; }
.taskido.unplannedFilter .year:not(.current):not([data-types*="unplanned"]) { display: none; }
.taskido.unplannedFilter .details:not(.today):not([data-types*="unplanned"]) { display: none; }
.taskido.unplannedFilter .task:not(.unplanned) { display: none; }

/*# sourceURL=app://obsidian.md/3_Archive/ETCs/Taskido/view.css */</style><div class="taskido noYear noDone noQuickEntry noFile noRepeat noHeader" id="taskido1722011098735"><span><div class="year current" data-types="due,scheduled,start,unplanned">2024</div><div class="details today" data-year="2024" data-types="scheduled unplanned"><span><div class="dateLine"><div class="date">Sat, Jul 27</div><div class="weekday"></div></div><div class="content"><div aria-label="Focus today" class="todayHeader">Today</div><div class="counters"><div aria-label="Filter tasks to do" id="todo" class="counter"><div class="count">5</div><div class="label">To Do</div></div><div aria-label="Filter overdue tasks" id="overdue" class="counter"><div class="count">0</div><div class="label">Overdue</div></div><div aria-label="Filter unplanned tasks" id="unplanned" class="counter"><div class="count">5</div><div class="label">Unplanned</div></div></div><div class="quickEntryPanel"><div class="left"><select aria-label="Select a note to add a new task to" class="fileSelect"><option value="2024-07-27.md" title="2024-07-27.md">📄&nbsp;2024-07-27</option><option value="3_Archive/32_Daily Notes/2024-05-21.md" title="3_Archive/32_Daily Notes/2024-05-21.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-05-21</option><option value="3_Archive/32_Daily Notes/2024-05-22.md" title="3_Archive/32_Daily Notes/2024-05-22.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-05-22</option><option value="3_Archive/32_Daily Notes/2024-06-10.md" title="3_Archive/32_Daily Notes/2024-06-10.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-06-10</option><option value="3_Archive/32_Daily Notes/2024-06-12.md" title="3_Archive/32_Daily Notes/2024-06-12.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-06-12</option><option value="3_Archive/32_Daily Notes/2024-06-24.md" title="3_Archive/32_Daily Notes/2024-06-24.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-06-24</option><option value="3_Archive/32_Daily Notes/2024-06-25.md" title="3_Archive/32_Daily Notes/2024-06-25.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-06-25</option><option value="3_Archive/32_Daily Notes/2024-07-05.md" title="3_Archive/32_Daily Notes/2024-07-05.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-05</option><option value="3_Archive/32_Daily Notes/2024-07-08.md" title="3_Archive/32_Daily Notes/2024-07-08.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-08</option><option value="3_Archive/32_Daily Notes/2024-07-10.md" title="3_Archive/32_Daily Notes/2024-07-10.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-10</option><option value="3_Archive/32_Daily Notes/2024-07-11.md" title="3_Archive/32_Daily Notes/2024-07-11.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-11</option><option value="3_Archive/32_Daily Notes/2024-07-18.md" title="3_Archive/32_Daily Notes/2024-07-18.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-18</option><option value="3_Archive/32_Daily Notes/2024-07-22.md" title="3_Archive/32_Daily Notes/2024-07-22.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-22</option><option value="3_Archive/32_Daily Notes/2024-07-23.md" title="3_Archive/32_Daily Notes/2024-07-23.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-23</option><option value="3_Archive/32_Daily Notes/2024-07-24.md" title="3_Archive/32_Daily Notes/2024-07-24.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-24</option><option value="3_Archive/32_Daily Notes/2024-07-26.md" title="3_Archive/32_Daily Notes/2024-07-26.md">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;2024-07-26</option><option value="3_Archive/32_Daily Notes/_Inbox.md" title="3_Archive/32_Daily Notes/_Inbox.md" selected="true">… / 📂&nbsp;32_Daily Notes / 📄&nbsp;_Inbox</option></select><input placeholder="Enter your tasks here" type="text" class="newTask"></div><div class="right"><button aria-label="Append new task to selected note" class="ok"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><polyline points="9 10 4 15 9 20"></polyline><path d="M20 4v7a4 4 0 0 1-4 4H4"></path></svg></button></div></div><div aria-label="2024-07-11" style="--task-color:var(--text-muted)" class="task scheduled" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-11.md" data-col="58" data-line="13"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-11.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 입학 통지서 자세히 확인   </div></a><div class="line info"><div aria-label="scheduled: 2024-07-24" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M5 22h14"></path><path d="M5 2h14"></path><path d="M17 22v-4.172a2 2 0 0 0-.586-1.414L12 12l-4.414 4.414A2 2 0 0 0 7 17.828V22"></path><path d="M7 2v4.172a2 2 0 0 0 .586 1.414L12 12l4.414-4.414A2 2 0 0 0 17 6.172V2"></path></svg></div><div class="label">3 days ago</div></div><div aria-label="" class="priority"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle><line y2="12" x2="12" y1="16" x1="12"></line><line y2="8" x2="12.01" y1="8" x1="12"></line></svg></div><div class="label">high priority</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-11.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-11<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#ETCs" style="--tag-color:#a374db;--tag-background:#a374db1a" class="tag" href="#Tags/a374db/ETCs" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">ETCs</div></a></div></div></div><div aria-label="2024-07-26" style="--task-color:var(--text-muted)" class="task scheduled" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-26.md" data-col="50" data-line="17"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-26.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 거미 몸통 위에서 아래로 관통하는 나사 추가 </div></a><div class="line info"><div aria-label="scheduled: 2024-07-27" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M5 22h14"></path><path d="M5 2h14"></path><path d="M17 22v-4.172a2 2 0 0 0-.586-1.414L12 12l-4.414 4.414A2 2 0 0 0 7 17.828V22"></path><path d="M7 2v4.172a2 2 0 0 0 .586 1.414L12 12l4.414-4.414A2 2 0 0 0 17 6.172V2"></path></svg></div><div class="label">Today</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-26.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-26<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a></div></div></div><div aria-label="2024-07-26" style="--task-color:var(--text-muted)" class="task scheduled" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-26.md" data-col="34" data-line="18"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-26.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 나인봇 전기테이프</div></a><div class="line info"><div aria-label="scheduled: 2024-07-27" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M5 22h14"></path><path d="M5 2h14"></path><path d="M17 22v-4.172a2 2 0 0 0-.586-1.414L12 12l-4.414 4.414A2 2 0 0 0 7 17.828V22"></path><path d="M7 2v4.172a2 2 0 0 0 .586 1.414L12 12l4.414-4.414A2 2 0 0 0 17 6.172V2"></path></svg></div><div class="label">Today</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-26.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-26<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a></div></div></div><div aria-label="2024-07-24" style="--task-color:var(--text-muted)" class="task scheduled" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-24.md" data-col="75" data-line="19"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-24.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 3D 프린터 구매요청서 마무리 후 건우 선배님께 전달  🔺 </div></a><div class="line info"><div aria-label="scheduled: 2024-07-26" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M5 22h14"></path><path d="M5 2h14"></path><path d="M17 22v-4.172a2 2 0 0 0-.586-1.414L12 12l-4.414 4.414A2 2 0 0 0 7 17.828V22"></path><path d="M7 2v4.172a2 2 0 0 0 .586 1.414L12 12l4.414-4.414A2 2 0 0 0 17 6.172V2"></path></svg></div><div class="label">a day ago</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-24.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-24<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#HERO" style="--tag-color:#ff443a;--tag-background:#ff443a1a" class="tag" href="#Tags/ff443a/HERO" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">HERO</div></a></div></div></div><div aria-label="2024-07-24" style="--task-color:var(--text-muted)" class="task unplanned" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-24.md" data-col="44" data-line="23"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-24.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 금도 시스템 견적서 정리 </div></a><div class="line info"><div aria-label="3_Archive/32_Daily Notes/2024-07-24.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-24<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#HERO" style="--tag-color:#ff443a;--tag-background:#ff443a1a" class="tag" href="#Tags/ff443a/HERO" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">HERO</div></a></div></div></div><div aria-label="2024-07-23" style="--task-color:var(--text-muted)" class="task unplanned" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-23.md" data-col="47" data-line="19"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-23.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 다이소 접이형 박스 3개 </div></a><div class="line info"><div aria-label="3_Archive/32_Daily Notes/2024-07-23.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-23<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#Shopping" style="--tag-color:#ffe880;--tag-background:#ffe8801a" class="tag" href="#Tags/ffe880/Shopping" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">Shopping</div></a></div></div></div><div aria-label="2024-07-18" style="--task-color:var(--text-muted)" class="task scheduled" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-18.md" data-col="50" data-line="21"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-18.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 장학금 확인  </div></a><div class="line info"><div aria-label="scheduled: 2024-07-24" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M5 22h14"></path><path d="M5 2h14"></path><path d="M17 22v-4.172a2 2 0 0 0-.586-1.414L12 12l-4.414 4.414A2 2 0 0 0 7 17.828V22"></path><path d="M7 2v4.172a2 2 0 0 0 .586 1.414L12 12l4.414-4.414A2 2 0 0 0 17 6.172V2"></path></svg></div><div class="label">3 days ago</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-18.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-18<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#ETCs" style="--tag-color:#a374db;--tag-background:#a374db1a" class="tag" href="#Tags/a374db/ETCs" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">ETCs</div></a></div></div></div><div aria-label="2024-07-10" style="--task-color:var(--text-muted)" class="task unplanned" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-10.md" data-col="48" data-line="11"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-10.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> Docker 끼리 ROS 통신 </div></a><div class="line info"><div aria-label="3_Archive/32_Daily Notes/2024-07-10.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-10<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#Study" style="--tag-color:#0c70f2;--tag-background:#0c70f21a" class="tag" href="#Tags/0c70f2/Study" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">Study</div></a></div></div></div><div aria-label="2024-06-25" style="--task-color:var(--text-muted)" class="task unplanned" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-06-25.md" data-col="42" data-line="28"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-06-25.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 라이다 센서 만저보기 </div></a><div class="line info"><div aria-label="3_Archive/32_Daily Notes/2024-06-25.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-06-25<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#Study" style="--tag-color:#0c70f2;--tag-background:#0c70f21a" class="tag" href="#Tags/0c70f2/Study" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">Study</div></a></div></div></div><div aria-label="2024-06-25" style="--task-color:var(--text-muted)" class="task unplanned" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-06-25.md" data-col="43" data-line="30"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-06-25.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> MAKE.md 살펴보기 </div></a><div class="line info"><div aria-label="3_Archive/32_Daily Notes/2024-06-25.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-06-25<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#Study" style="--tag-color:#0c70f2;--tag-background:#0c70f21a" class="tag" href="#Tags/0c70f2/Study" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">Study</div></a></div></div></div></div></span></div><div class="details " data-year="2024" data-types="start"><span><div class="dateLine"><div class="date">Tue, Aug 6</div><div class="weekday"></div></div><div class="content"><div aria-label="2024-06-10" style="--task-color:var(--text-muted)" class="task start" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-06-10.md" data-col="74" data-line="27"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-06-10.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 💸포항공대 등록금 납부    </div></a><div class="line info"><div aria-label="start: 2024-08-08" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><rect ry="2" rx="2" height="18" width="18" y="4" x="3"></rect><line y2="6" x2="16" y1="2" x1="16"></line><line y2="6" x2="8" y1="2" x1="8"></line><line y2="10" x2="21" y1="10" x1="3"></line></svg></div><div class="label">in 12 days</div></div><div aria-label="start: 2024-08-06" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M17.8 19.2 16 11l3.5-3.5C21 6 21.5 4 21 3c-1-.5-3 0-4.5 1.5L13 8 4.8 6.2c-.5-.1-.9.1-1.1.5l-.3.5c-.2.5-.1 1 .3 1.3L9 12l-2 3H4l-1 1 3 2 2 3 1-1v-3l3-2 3.5 5.3c.3.4.8.5 1.3.3l.5-.2c.4-.3.6-.7.5-1.2z"></path></svg></div><div class="label">in 10 days</div></div><div aria-label="" class="priority"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle><line y2="12" x2="12" y1="16" x1="12"></line><line y2="8" x2="12.01" y1="8" x1="12"></line></svg></div><div class="label">high priority</div></div><div aria-label="3_Archive/32_Daily Notes/2024-06-10.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-06-10<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#ETCs" style="--tag-color:#a374db;--tag-background:#a374db1a" class="tag" href="#Tags/a374db/ETCs" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">ETCs</div></a></div></div></div></div></span></div><div class="details " data-year="2024" data-types="due"><span><div class="dateLine"><div class="date">Thu, Aug 8</div><div class="weekday"></div></div><div class="content"><div aria-label="2024-06-10" style="--task-color:var(--text-muted)" class="task due" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-06-10.md" data-col="74" data-line="27"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-06-10.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 💸포항공대 등록금 납부    </div></a><div class="line info"><div aria-label="due: 2024-08-08" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><rect ry="2" rx="2" height="18" width="18" y="4" x="3"></rect><line y2="6" x2="16" y1="2" x1="16"></line><line y2="6" x2="8" y1="2" x1="8"></line><line y2="10" x2="21" y1="10" x1="3"></line></svg></div><div class="label">in 12 days</div></div><div aria-label="due: 2024-08-06" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M17.8 19.2 16 11l3.5-3.5C21 6 21.5 4 21 3c-1-.5-3 0-4.5 1.5L13 8 4.8 6.2c-.5-.1-.9.1-1.1.5l-.3.5c-.2.5-.1 1 .3 1.3L9 12l-2 3H4l-1 1 3 2 2 3 1-1v-3l3-2 3.5 5.3c.3.4.8.5 1.3.3l.5-.2c.4-.3.6-.7.5-1.2z"></path></svg></div><div class="label">in 10 days</div></div><div aria-label="" class="priority"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle><line y2="12" x2="12" y1="16" x1="12"></line><line y2="8" x2="12.01" y1="8" x1="12"></line></svg></div><div class="label">high priority</div></div><div aria-label="3_Archive/32_Daily Notes/2024-06-10.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-06-10<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#ETCs" style="--tag-color:#a374db;--tag-background:#a374db1a" class="tag" href="#Tags/a374db/ETCs" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">ETCs</div></a></div></div></div></div></span></div><div class="details " data-year="2024" data-types="start"><span><div class="dateLine"><div class="date">Fri, Aug 9</div><div class="weekday"></div></div><div class="content"><div aria-label="2024-07-11" style="--task-color:var(--text-muted)" class="task start" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-11.md" data-col="65" data-line="14"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-11.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 해양 박람회   </div></a><div class="line info"><div aria-label="start: 2024-08-12" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><rect ry="2" rx="2" height="18" width="18" y="4" x="3"></rect><line y2="6" x2="16" y1="2" x1="16"></line><line y2="6" x2="8" y1="2" x1="8"></line><line y2="10" x2="21" y1="10" x1="3"></line></svg></div><div class="label">in 16 days</div></div><div aria-label="start: 2024-08-09" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M17.8 19.2 16 11l3.5-3.5C21 6 21.5 4 21 3c-1-.5-3 0-4.5 1.5L13 8 4.8 6.2c-.5-.1-.9.1-1.1.5l-.3.5c-.2.5-.1 1 .3 1.3L9 12l-2 3H4l-1 1 3 2 2 3 1-1v-3l3-2 3.5 5.3c.3.4.8.5 1.3.3l.5-.2c.4-.3.6-.7.5-1.2z"></path></svg></div><div class="label">in 13 days</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-11.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-11<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#HERO" style="--tag-color:#ff443a;--tag-background:#ff443a1a" class="tag" href="#Tags/ff443a/HERO" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">HERO</div></a></div></div></div></div></span></div><div class="details " data-year="2024" data-types="due"><span><div class="dateLine"><div class="date">Mon, Aug 12</div><div class="weekday"></div></div><div class="content"><div aria-label="2024-07-11" style="--task-color:var(--text-muted)" class="task due" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-11.md" data-col="65" data-line="14"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-11.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 해양 박람회   </div></a><div class="line info"><div aria-label="due: 2024-08-12" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><rect ry="2" rx="2" height="18" width="18" y="4" x="3"></rect><line y2="6" x2="16" y1="2" x1="16"></line><line y2="6" x2="8" y1="2" x1="8"></line><line y2="10" x2="21" y1="10" x1="3"></line></svg></div><div class="label">in 16 days</div></div><div aria-label="due: 2024-08-09" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M17.8 19.2 16 11l3.5-3.5C21 6 21.5 4 21 3c-1-.5-3 0-4.5 1.5L13 8 4.8 6.2c-.5-.1-.9.1-1.1.5l-.3.5c-.2.5-.1 1 .3 1.3L9 12l-2 3H4l-1 1 3 2 2 3 1-1v-3l3-2 3.5 5.3c.3.4.8.5 1.3.3l.5-.2c.4-.3.6-.7.5-1.2z"></path></svg></div><div class="label">in 13 days</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-11.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-11<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#HERO" style="--tag-color:#ff443a;--tag-background:#ff443a1a" class="tag" href="#Tags/ff443a/HERO" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">HERO</div></a></div></div></div></div></span></div><div class="details " data-year="2024" data-types="scheduled"><span><div class="dateLine"><div class="date">Fri, Aug 16</div><div class="weekday"></div></div><div class="content"><div aria-label="2024-07-18" style="--task-color:var(--text-muted)" class="task scheduled" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-18.md" data-col="57" data-line="15"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-18.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 작계훈련  </div></a><div class="line info"><div aria-label="scheduled: 2024-08-16" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M5 22h14"></path><path d="M5 2h14"></path><path d="M17 22v-4.172a2 2 0 0 0-.586-1.414L12 12l-4.414 4.414A2 2 0 0 0 7 17.828V22"></path><path d="M7 2v4.172a2 2 0 0 0 .586 1.414L12 12l4.414-4.414A2 2 0 0 0 17 6.172V2"></path></svg></div><div class="label">in 20 days</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-18.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-18<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#TIME/1300-1900" style="--tag-color:#0a3711;--tag-background:#0a37111a" class="tag" href="#Tags/0a3711/TIME/1300-1900" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">TIME/1300-1900</div></a></div></div></div></div></span></div><div class="details " data-year="2024" data-types="start"><span><div class="dateLine"><div class="date">Sun, Sep 1</div><div class="weekday"></div></div><div class="content"><div aria-label="2024-07-18" style="--task-color:var(--text-muted)" class="task start" data-dailynote="true" data-link="3_Archive/32_Daily Notes/2024-07-18.md" data-col="48" data-line="20"><div class="timeline"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><circle r="10" cy="12" cx="12"></circle></svg></div><div class="stripe"></div></div><div class="lines"><a href="3_Archive/32_Daily Notes/2024-07-18.md" class="internal-link" target="_blank" rel="noopener"><div class="content"> 안전교육  </div></a><div class="line info"><div aria-label="start: 2024-09-01" class="relative"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M17.8 19.2 16 11l3.5-3.5C21 6 21.5 4 21 3c-1-.5-3 0-4.5 1.5L13 8 4.8 6.2c-.5-.1-.9.1-1.1.5l-.3.5c-.2.5-.1 1 .3 1.3L9 12l-2 3H4l-1 1 3 2 2 3 1-1v-3l3-2 3.5 5.3c.3.4.8.5 1.3.3l.5-.2c.4-.3.6-.7.5-1.2z"></path></svg></div><div class="label">in a month</div></div><div aria-label="3_Archive/32_Daily Notes/2024-07-18.md" class="file"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"></path><polyline points="14 2 14 8 20 8"></polyline><line y2="13" x2="8" y1="13" x1="16"></line><line y2="17" x2="8" y1="17" x1="16"></line><line y2="9" x2="8" y1="9" x1="10"></line></svg></div><div class="label">2024-07-18<span class="header"> &gt; undefined</span></div></div><a aria-label="#task" style="--tag-color:var(--text-muted)" class="tag" href="#task" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">task</div></a><a aria-label="#HERO" style="--tag-color:#ff443a;--tag-background:#ff443a1a" class="tag" href="#Tags/ff443a/HERO" target="_blank" rel="noopener"><div class="icon"><svg stroke-linejoin="round" stroke-linecap="round" stroke-width="2" stroke="currentColor" fill="none" viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2H2v10l9.29 9.29c.94.94 2.48.94 3.42 0l6.58-6.58c.94-.94.94-2.48 0-3.42L12 2Z"></path><path d="M7 7h.01"></path></svg></div><div class="label">HERO</div></a></div></div></div></div></span></div></span></div>