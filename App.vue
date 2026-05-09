<script setup>
import { Button, Badge, Alert, TextInput, Textarea, Combobox, Select, MultiSelect, DatePicker, TimePicker, MonthPicker, TabButtons, TextEditor, Slider, Password, Tooltip, Progress, Popover, FormControl, ErrorMessage, Dropdown, Sidebar, ListView, Avatar, Breadcrumbs, AxisChart, DonutChart, FunnelChart, NumberChart, Calendar, Tabs, Switch, CommandPalette } from './src'
import { ref } from 'vue'

const isDark = ref(false)

function toggleTheme() {
  isDark.value = !isDark.value
  document.documentElement.setAttribute(
    'data-theme',
    isDark.value ? 'dark' : 'light'
  )
}
const showCommandPalette = ref(false)
const commandSearch = ref('')
const commandGroups = ref([
  {
    title: 'Navigation',
    component: {
      template: `
        <div class="flex w-full min-w-0 items-center rounded px-2 py-2 text-base font-medium text-ink-gray-8" :class="{ 'bg-surface-blueprint-2': active }">
          <span class="overflow-hidden text-ellipsis whitespace-nowrap">{{ item.title }}</span>
          <span v-if="item.description" class="ml-auto whitespace-nowrap pl-2 text-ink-gray-5">{{ item.description }}</span>
        </div>
      `,
      props: ['item', 'active'],
    },
    items: [
      { name: '1', title: 'Go to Dashboard', description: 'Home' },
      { name: '2', title: 'Go to Projects', description: 'Projects' },
      { name: '3', title: 'Go to Finance', description: 'Finance' },
    ],
  },
  {
    title: 'Recent',
    component: {
      template: `
        <div class="flex w-full min-w-0 items-center rounded px-2 py-2 text-base font-medium text-ink-gray-8" :class="{ 'bg-surface-blueprint-2': active }">
          <span class="overflow-hidden text-ellipsis whitespace-nowrap">{{ item.title }}</span>
          <span v-if="item.description" class="ml-auto whitespace-nowrap pl-2 text-ink-gray-5">{{ item.description }}</span>
        </div>
      `,
      props: ['item', 'active'],
    },
    items: [
      { name: '4', title: 'Project Alpha', description: 'Project' },
      { name: '5', title: 'Invoice #1234', description: 'Finance' },
    ],
  },
])
const formControlText = ref('')
const formControlSelect = ref('')
const formControlCombobox = ref('')
const formControlTextarea = ref('')
const dropdownValue = ref('')
const showError = ref(true)
const dropdownOptions = ref([
  { label: 'Edit', onClick: () => console.log('Edit clicked') },
  { label: 'Duplicate', onClick: () => console.log('Duplicate clicked') },
  { label: 'Delete', theme: 'red', onClick: () => console.log('Delete clicked') },
])
const listFilterValue = ref({})
const docfields = ref([
  { label: 'Name', fieldname: 'name', fieldtype: 'Data' },
  { label: 'Status', fieldname: 'status', fieldtype: 'Select', options: 'Active\nInactive\nPending' },
  { label: 'Amount', fieldname: 'amount', fieldtype: 'Float' },
  { label: 'Is Active', fieldname: 'is_active', fieldtype: 'Check' },
])
const timePickerValue = ref('')
const timePickerValue2 = ref('09:00')
const timePickerValue3 = ref('')
const datePickerValue = ref('')
const sliderValue = ref([30])
const sliderValue2 = ref([60])
const sliderRangeValue = ref([20, 80])

const sections = ref([
  {
    label: 'Main',
    items: [
      { label: 'Home', suffix: '8', isActive: true, onClick: () => setActive('Home') },
      { label: 'User', suffix: '4', isActive: false, onClick: () => setActive('User') },
      { label: 'Notification', isActive: false, onClick: () => setActive('Notification') },
    ],
  },
  {
    label: 'Finance',
    collapsible: true,
    items: [
      { label: 'Invoice', suffix: '8', isActive: false, onClick: () => setActive('Invoice') },
      { label: 'Payments', suffix: '8', isActive: false, onClick: () => setActive('Payments') },
    ],
  },
])

const tabButtonValue = ref('overview')
const tabButtonValue2 = ref('day')
const tabButtonValue3 = ref('day')
const tabButtonValue4 = ref('overview')
function setActive(label) {
  sections.value.forEach(section => {
    section.items.forEach(item => {
      item.isActive = item.label === label
    })
  })
}
const passwordValue = ref('')
const passwordValue2 = ref('')

const columns = ref([
  { label: 'Name', key: 'name', width: '200px' },
  { label: 'Email', key: 'email', width: '220px' },
  { label: 'Role', key: 'role', width: '150px' },
  { label: 'Status', key: 'status', width: '120px' },
])
const textEditorContent = ref('<p>Start typing here...</p>')

const rows = ref([
  { id: 1, name: 'John Doe', email: 'john@doe.com', role: 'Developer', status: 'Active' },
  { id: 2, name: 'Jane Smith', email: 'jane@smith.com', role: 'Designer', status: 'Active' },
  { id: 3, name: 'Bob Wilson', email: 'bob@wilson.com', role: 'Manager', status: 'Inactive' },
  { id: 4, name: 'Alice Brown', email: 'alice@brown.com', role: 'Developer', status: 'Active' },
  { id: 5, name: 'Charlie Davis', email: 'charlie@davis.com', role: 'Designer', status: 'Active' },
])
const multiSelectValue = ref([])
const multiSelectOptions = ref([
  { label: 'Project Management', value: 'pm' },
  { label: 'Finance', value: 'finance' },
  { label: 'Procurement', value: 'procurement' },
  { label: 'HR', value: 'hr' },
  { label: 'CRM', value: 'crm' },
])
const monthPickerValue = ref('')
const monthPickerValue2 = ref('January 2026')

const subtleValue = ref('')
const outlineValue = ref('')
const prefixValue = ref('')
const suffixValue = ref('')
const ghostValue = ref('')
</script>

<template>
  <div
    style="display: flex; height: 100vh; font-family: Avenir, sans-serif;"
    :data-theme="isDark ? 'dark' : 'light'"
  >
    <Sidebar
      :header="{ title: 'Intrakore', subtitle: 'admin@intrakore.com' }"
      :sections="sections"
    />

    <div style="flex: 1; overflow-y: auto; padding: 40px; display: flex; flex-direction: column; gap: 32px; background: var(--surface-white);">

      <!-- Header -->
      <div style="display: flex; justify-content: space-between; align-items: center;">
        <h1 style="font-size: 28px; font-weight: 900; font-family: 'ITC Avant Garde Gothic Pro'; color: var(--text-ink-gray-9);">
          Intrakore Design Preview
        </h1>
        <button
          @click="toggleTheme"
          style="padding: 8px 20px; border-radius: 6px; background: #000FCC; color: white; border: none; cursor: pointer; font-family: Avenir, sans-serif;"
        >
          {{ isDark ? '☀️ Light Mode' : '🌙 Dark Mode' }}
        </button>
      </div>

      <!-- Buttons — Blueprint -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">BUTTONS — BLUEPRINT</p>
        <div style="display: flex; gap: 12px; flex-wrap: wrap;">
          <Button variant="solid" theme="blueprint">Solid</Button>
          <Button variant="subtle" theme="blueprint">Subtle</Button>
          <Button variant="outline" theme="blueprint">Outline</Button>
          <Button variant="ghost" theme="blueprint">Ghost</Button>
          <Button variant="solid" theme="blueprint" :disabled="true">Disabled</Button>
          <Button variant="solid" theme="blueprint" :loading="true">Loading</Button>
        </div>
      </div>

      <!-- Buttons — Gray -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">BUTTONS — GRAY</p>
        <div style="display: flex; gap: 12px; flex-wrap: wrap;">
          <Button variant="solid" theme="gray">Solid</Button>
          <Button variant="subtle" theme="gray">Subtle</Button>
          <Button variant="outline" theme="gray">Outline</Button>
          <Button variant="ghost" theme="gray">Ghost</Button>
          <Button variant="solid" theme="gray" :disabled="true">Disabled</Button>
        </div>
      </div>

      <!-- List View -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">LIST VIEW</p>
        <ListView
          :columns="columns"
          :rows="rows"
          row-key="id"
          :options="{ selectable: true, showTooltip: true }"
        />
      </div>

      <!-- Badges -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">BADGES</p>
        <div style="display: flex; gap: 12px; flex-wrap: wrap;">
          <Badge theme="blueprint" variant="subtle">Subtle</Badge>
          <Badge theme="blueprint" variant="solid">Solid</Badge>
          <Badge theme="blueprint" variant="outline">Outline</Badge>
          <Badge theme="blueprint" variant="ghost">Ghost</Badge>
          <Badge theme="gray">Neutral</Badge>
          <Badge theme="red">Error</Badge>
          <Badge theme="green">Success</Badge>
        </div>
      </div>

      <!-- Alerts -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">ALERTS</p>
        <div style="display: flex; flex-direction: column; gap: 12px;">
          <Alert title="Blueprint Info" theme="blue" variant="subtle">Blueprint info state</Alert>
          <Alert title="Success State" theme="green" variant="subtle">Clearing green for success</Alert>
          <Alert title="Warning State" theme="yellow" variant="subtle">Amber for warnings</Alert>
          <Alert title="Error State" theme="red" variant="subtle">Red for errors</Alert>
        </div>
      </div>

      <!-- Text Input — Subtle -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">TEXT INPUT — SUBTLE</p>
        <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">
          <TextInput variant="subtle" size="sm" placeholder="Default (sm)" v-model="subtleValue" />
          <TextInput variant="subtle" size="md" placeholder="Default (md)" v-model="subtleValue" />
          <TextInput variant="subtle" size="lg" placeholder="Default (lg)" v-model="subtleValue" />
          <TextInput variant="subtle" size="sm" placeholder="Disabled" :disabled="true" />
        </div>
      </div>

      <!-- Text Input — Outline -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">TEXT INPUT — OUTLINE</p>
        <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">
          <TextInput variant="outline" size="sm" placeholder="Default (sm)" v-model="outlineValue" />
          <TextInput variant="outline" size="md" placeholder="Default (md)" v-model="outlineValue" />
          <TextInput variant="outline" size="lg" placeholder="Default (lg)" v-model="outlineValue" />
          <TextInput variant="outline" size="sm" placeholder="Disabled" :disabled="true" />
        </div>
      </div>

      <!-- Text Input — Prefix / Suffix -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">TEXT INPUT — PREFIX / SUFFIX</p>
        <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">
          <TextInput variant="subtle" size="md" placeholder="Search..." v-model="prefixValue">
            <template #prefix>
              <svg style="width:16px;height:16px;" viewBox="0 0 16 16" fill="none">
                <circle cx="7" cy="7" r="4.5" stroke="currentColor" stroke-width="1.5"/>
                <path d="M10.5 10.5L13 13" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
              </svg>
            </template>
          </TextInput>
          <TextInput variant="outline" size="md" placeholder="Enter email" v-model="suffixValue">
            <template #suffix>
              <svg style="width:16px;height:16px;" viewBox="0 0 16 16" fill="none">
                <rect x="2" y="4" width="12" height="9" rx="1.5" stroke="currentColor" stroke-width="1.5"/>
                <path d="M2 6l6 4 6-4" stroke="currentColor" stroke-width="1.5"/>
              </svg>
            </template>
          </TextInput>
        </div>
      </div>

      <!-- Avatar -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">AVATAR</p>
        <div style="display: flex; gap: 12px; align-items: center; flex-wrap: wrap;">
          <Avatar size="xs" label="Shaistha" />
          <Avatar size="sm" label="Shaistha" />
          <Avatar size="md" label="Shaistha" />
          <Avatar size="lg" label="Shaistha" />
          <Avatar size="xl" label="Shaistha" />
          <Avatar size="2xl" label="Shaistha" />
          <Avatar size="3xl" label="Shaistha" />
        </div>
        <div style="display: flex; gap: 12px; align-items: center; flex-wrap: wrap; margin-top: 12px;">
          <Avatar size="md" shape="square" label="Shaistha" />
          <Avatar size="xl" shape="square" label="Shaistha" />
          <Avatar size="2xl" shape="square" label="Shaistha" />
          <Avatar size="2xl" label="Shaistha" image="https://avatars.githubusercontent.com/u/9355208" />
        </div>
      </div>

      <!-- Breadcrumbs -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">BREADCRUMBS</p>
        <Breadcrumbs
          :items="[
            { label: 'Home', route: '/' },
            { label: 'Projects', route: '/' },
            { label: 'Intrakore ERP' },
          ]"
        />
      </div>

      <!-- Number Chart -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">NUMBER CHART</p>
        <div style="display: flex; gap: 12px; flex-wrap: wrap;">
          <NumberChart :config="{
            title: 'Total Revenue',
            value: 1250000,
            prefix: 'AED',
            delta: 12.5,
            deltaPrefix: '+',
            deltaSuffix: '%'
          }" style="width: 200px; border: 1px solid var(--outline-blueprint-2); border-radius: 8px;" />
          <NumberChart :config="{
            title: 'Lost Deals',
            value: 45000,
            prefix: 'AED',
            delta: -5.2,
            deltaSuffix: '%'
          }" style="width: 200px; border: 1px solid var(--outline-blueprint-2); border-radius: 8px;" />
        </div>
      </div>

      <!-- Axis Chart -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">AXIS CHART</p>
        <AxisChart :config="{
          title: 'Monthly Revenue',
          colors: ['#000FCE', '#705CFF', '#68C2A3'],
          xAxis: { key: 'month', type: 'category' },
          yAxis: { title: 'Revenue' },
          series: [{ name: 'revenue', type: 'bar' }],
          data: [
            { month: 'Jan', revenue: 120000 },
            { month: 'Feb', revenue: 180000 },
            { month: 'Mar', revenue: 150000 },
            { month: 'Apr', revenue: 210000 },
            { month: 'May', revenue: 190000 },
            { month: 'Jun', revenue: 240000 },
          ]
        }" style="height: 300px;" />
      </div>

      <!-- Donut Chart -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">DONUT CHART</p>
        <DonutChart :config="{
          title: 'Deal Status',
          colors: ['#000FCE', '#705CFF', '#68C2A3', '#8D95F6'],
          categoryColumn: 'status',
          valueColumn: 'count',
          data: [
            { status: 'Won', count: 45 },
            { status: 'Lost', count: 20 },
            { status: 'Active', count: 30 },
            { status: 'Pending', count: 5 },
          ]
        }" style="height: 300px;" />
      </div>

      <!-- Funnel Chart -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">FUNNEL CHART</p>
        <FunnelChart :config="{
          title: 'Sales Pipeline',
          categoryColumn: 'stage',
          valueColumn: 'count',
          data: [
            { stage: 'Leads', count: 100 },
            { stage: 'Qualified', count: 75 },
            { stage: 'Proposal', count: 50 },
            { stage: 'Negotiation', count: 30 },
            { stage: 'Won', count: 15 },
          ]
        }" style="height: 300px;" />
      </div>

      <!-- Calendar -->
      <div>
        <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">CALENDAR</p>
        <div style="height: 600px;">
          <Calendar
            :events="[
              { id: '1', title: 'Project Kickoff', fromDate: '2026-04-23', toDate: '2026-04-23', fromTime: '09:00:00', toTime: '10:00:00', color: '#000FCE' },
              { id: '2', title: 'Design Review', fromDate: '2026-04-24', toDate: '2026-04-24', fromTime: '14:00:00', toTime: '15:00:00', color: '#705CFF' },
              { id: '3', title: 'Client Meeting', fromDate: '2026-04-25', toDate: '2026-04-25', fromTime: '11:00:00', toTime: '12:00:00', color: '#68C2A3' },
            ]"
          />
        </div>
      </div>
      <div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">TABS</p>
  <Tabs
    :tabs="[
      { label: 'Overview' },
      { label: 'Activity' },
      { label: 'Documents' },
      { label: 'Settings' },
    ]"
  />
</div>
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">SWITCH</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">
    <Switch label="Enable notifications" />
    <Switch label="Dark mode" :modelValue="true" />
    <Switch label="Disabled" :disabled="true" />
    <Switch label="With description" description="This setting controls something important" />
  </div>
</div>
<!-- Date Picker -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">DATE PICKER</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">
    <DatePicker variant="subtle" placeholder="Select date (subtle)" v-model="datePickerValue" />
    <DatePicker variant="outline" placeholder="Select date (outline)" v-model="datePickerValue" />
    <DatePicker variant="subtle" placeholder="Disabled" :disabled="true" />
    <DatePicker variant="subtle" placeholder="With clear" :clearable="true" v-model="datePickerValue" />
  </div>
</div>
<!-- Tab Buttons -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">TAB BUTTONS</p>
  <div style="display: flex; flex-direction: column; gap: 16px; max-width: 400px;">

    <!-- Text only -->
    <TabButtons
      :buttons="[
        { label: 'Overview', value: 'overview' },
        { label: 'Activity', value: 'activity' },
        { label: 'Documents', value: 'documents' },
      ]"
      v-model="tabButtonValue"
    />

    <!-- With icons -->
    <TabButtons
      :buttons="[
        { label: 'Day', value: 'day', iconLeft: 'calendar' },
        { label: 'Week', value: 'week', iconLeft: 'calendar' },
        { label: 'Month', value: 'month', iconLeft: 'calendar' },
      ]"
      v-model="tabButtonValue2"
    />

    <!-- Icons only -->
    <TabButtons
      :buttons="[
        { label: 'Day', value: 'day', iconLeft: 'calendar', hideLabel: true },
        { label: 'Week', value: 'week', iconLeft: 'list', hideLabel: true },
        { label: 'Month', value: 'month', iconLeft: 'grid', hideLabel: true },
      ]"
      v-model="tabButtonValue3"
    />

    <!-- With disabled -->
    <TabButtons
      :buttons="[
        { label: 'Overview', value: 'overview' },
        { label: 'Activity', value: 'activity', disabled: true },
        { label: 'Documents', value: 'documents' },
      ]"
      v-model="tabButtonValue4"
    />

  </div>
</div>
<!-- Time Picker -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">TIME PICKER</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">

    <!-- Subtle -->
    <TimePicker
      variant="subtle"
      placeholder="Select time (subtle)"
      v-model="timePickerValue"
    />

    <!-- Outline -->
    <TimePicker
      variant="outline"
      placeholder="Select time (outline)"
      v-model="timePickerValue2"
    />

    <!-- 24 hour -->
    <TimePicker
      variant="subtle"
      placeholder="24 hour format"
      :use12Hour="false"
      v-model="timePickerValue3"
    />

    <!-- Disabled -->
    <TimePicker
      variant="subtle"
      placeholder="Disabled"
      :disabled="true"
    />

    <!-- With interval -->
    <TimePicker
      variant="outline"
      placeholder="30 min intervals"
      :interval="30"
      v-model="timePickerValue"
    />

  </div>
</div>
<!-- Text Editor -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">TEXT EDITOR</p>
  <div style="max-width: 800px; border: 1px solid var(--outline-gray-2); border-radius: 8px; overflow: hidden;">
    <TextEditor
      v-model:content="textEditorContent"
      :fixedMenu="true"
      :editable="true"
      placeholder="Start typing..."
      editorClass="prose-sm"
    />
  </div>
</div>
<!-- Slider -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">SLIDER</p>
  <div style="display: flex; flex-direction: column; gap: 20px; max-width: 400px;">

    <!-- Default sm -->
    <Slider
      size="sm"
      label="Volume (sm)"
      v-model="sliderValue"
      :min="0"
      :max="100"
      :step="1"
    />

    <!-- md size -->
    <Slider
      size="md"
      label="Brightness (md)"
      v-model="sliderValue2"
      :min="0"
      :max="100"
      :step="1"
    />

    <!-- Range -->
    <Slider
      size="sm"
      label="Price Range"
      v-model="sliderRangeValue"
      :min="0"
      :max="100"
      :step="5"
    />

    <!-- Disabled -->
    <Slider
      size="sm"
      label="Disabled"
      v-model="sliderValue"
      :disabled="true"
    />

    <!-- With description -->
    <Slider
      size="md"
      label="With description"
      description="Adjust the value between 0 and 100"
      v-model="sliderValue"
      :min="0"
      :max="100"
    />

  </div>
</div>
<!-- Password -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">PASSWORD</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">

    <!-- Subtle sm -->
    <Password
      size="sm"
      variant="subtle"
      label="Password (subtle sm)"
      placeholder="Enter password"
      v-model="passwordValue"
    />

    <!-- Outline sm -->
    <Password
      size="sm"
      variant="outline"
      label="Password (outline sm)"
      placeholder="Enter password"
      v-model="passwordValue2"
    />

    <!-- md -->
    <Password
      size="md"
      variant="subtle"
      label="Password (md)"
      placeholder="Enter password"
      v-model="passwordValue"
    />

    <!-- Disabled -->
    <Password
      size="sm"
      variant="subtle"
      label="Disabled"
      placeholder="Disabled"
      :disabled="true"
    />

    <!-- With description -->
    <Password
      size="sm"
      variant="subtle"
      label="With description"
      description="Must be at least 8 characters"
      placeholder="Enter password"
      v-model="passwordValue"
    />

  </div>
</div>
<!-- Tooltip -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">TOOLTIP</p>
  <div style="display: flex; gap: 24px; flex-wrap: wrap; align-items: center;">

    <!-- Top (default) -->
    <Tooltip text="This is a tooltip" side="top">
      <Button variant="outline" theme="blueprint">Hover me (top)</Button>
    </Tooltip>

    <!-- Bottom -->
    <Tooltip text="Tooltip on bottom" side="bottom">
      <Button variant="outline" theme="blueprint">Hover me (bottom)</Button>
    </Tooltip>

    <!-- Left -->
    <Tooltip text="Tooltip on left" side="left">
      <Button variant="outline" theme="blueprint">Hover me (left)</Button>
    </Tooltip>

    <!-- Right -->
    <Tooltip text="Tooltip on right" side="right">
      <Button variant="outline" theme="blueprint">Hover me (right)</Button>
    </Tooltip>

    <!-- Custom content slot -->
    <Tooltip side="top">
      <Button variant="subtle" theme="blueprint">Custom tooltip</Button>
      <template #content>
        <span style="font-weight: 500;">Custom</span> tooltip content
      </template>
    </Tooltip>

  </div>
</div>
<!-- Select -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">SELECT</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">
    <Select size="sm" variant="subtle" placeholder="Select module (subtle sm)" :options="selectOptions" v-model="selectValue" />
    <Select size="md" variant="subtle" placeholder="Select module (subtle md)" :options="selectOptions" v-model="selectValue" />
    <Select size="sm" variant="outline" placeholder="Select module (outline sm)" :options="selectOptions" v-model="selectValue" />
    <Select size="md" variant="outline" placeholder="Select module (outline md)" :options="selectOptions" v-model="selectValue" />
    <Select size="sm" variant="ghost" placeholder="Select module (ghost)" :options="selectOptions" v-model="selectValue" />
    <Select size="sm" variant="subtle" placeholder="Disabled" :options="selectOptions" :disabled="true" />
  </div>
</div>

<!-- Combobox -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">COMBOBOX</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">
    <Combobox size="sm" variant="subtle" placeholder="Select module (subtle sm)" :options="comboboxOptions" v-model="comboboxValue" />
    <Combobox size="md" variant="subtle" placeholder="Select module (subtle md)" :options="comboboxOptions" v-model="comboboxValue" />
    <Combobox size="sm" variant="outline" placeholder="Select module (outline sm)" :options="comboboxOptions" v-model="comboboxValue" />
    <Combobox size="md" variant="outline" placeholder="Select module (outline md)" :options="comboboxOptions" v-model="comboboxValue" />
    <Combobox size="sm" variant="subtle" placeholder="Disabled" :options="comboboxOptions" :disabled="true" />
    <Combobox trigger="button" variant="subtle" placeholder="Button mode" :options="comboboxOptions" v-model="comboboxValue" />
  </div>
</div>
<Combobox trigger="button" variant="subtle" placeholder="Button mode" :options="comboboxOptions" v-model="comboboxValue" />
<!-- MultiSelect -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">MULTI SELECT</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">

    <!-- Subtle sm -->
    <MultiSelect
      size="sm"
      variant="subtle"
      placeholder="Select modules (subtle sm)"
      :options="multiSelectOptions"
      v-model="multiSelectValue"
    />

    <!-- Outline sm -->
    <MultiSelect
      size="sm"
      variant="outline"
      placeholder="Select modules (outline sm)"
      :options="multiSelectOptions"
      v-model="multiSelectValue"
    />

    <!-- md -->
    <MultiSelect
      size="md"
      variant="subtle"
      placeholder="Select modules (md)"
      :options="multiSelectOptions"
      v-model="multiSelectValue"
    />

    <!-- Disabled -->
    <MultiSelect
      size="sm"
      variant="subtle"
      placeholder="Disabled"
      :options="multiSelectOptions"
      :disabled="true"
    />

    <!-- Hide search -->
    <MultiSelect
      size="sm"
      variant="subtle"
      placeholder="No search"
      :options="multiSelectOptions"
      :hideSearch="true"
      v-model="multiSelectValue"
    />

  </div>
</div>
<!-- Month Picker -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">MONTH PICKER</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">

    <!-- Empty -->
    <MonthPicker
      placeholder="Select month"
      v-model="monthPickerValue"
    />

    <!-- With value -->
    <MonthPicker
      placeholder="Select month"
      v-model="monthPickerValue2"
    />

    <!-- Disabled -->
    <MonthPicker
      placeholder="Disabled"
      :disabled="true"
    />

  </div>
</div>
<!-- Progress -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">PROGRESS</p>
  <div style="display: flex; flex-direction: column; gap: 20px; max-width: 400px;">

    <!-- sm -->
    <Progress size="sm" :value="40" label="Loading (sm)" :hint="true" />

    <!-- md -->
    <Progress size="md" :value="60" label="Loading (md)" :hint="true" />

    <!-- lg -->
    <Progress size="lg" :value="75" label="Loading (lg)" :hint="true" />

    <!-- xl -->
    <Progress size="xl" :value="90" label="Loading (xl)" :hint="true" />

    <!-- No label -->
    <Progress size="md" :value="50" />

    <!-- Intervals sm -->
    <Progress size="sm" :value="40" label="Intervals (sm)" :intervals="true" :intervalCount="6" :hint="true" />

    <!-- Intervals md -->
    <Progress size="md" :value="60" label="Intervals (md)" :intervals="true" :intervalCount="8" :hint="true" />

    <!-- Full -->
    <Progress size="md" :value="100" label="Complete" :hint="true" />

    <!-- Empty -->
    <Progress size="md" :value="0" label="Not started" :hint="true" />

  </div>
</div>
<!-- Popover -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">POPOVER</p>
  <div style="display: flex; gap: 24px; flex-wrap: wrap; align-items: flex-start;">

    <!-- Basic click -->
    <Popover placement="bottom-start">
      <template #target="{ togglePopover }">
        <Button variant="outline" theme="blueprint" @click="togglePopover">
          Click me
        </Button>
      </template>
      <template #body>
        <div style="padding: 16px; min-width: 200px;">
          <p style="font-size: 14px; color: var(--ink-blueprint-4); margin-bottom: 8px; font-weight: 500;">Popover Title</p>
          <p style="font-size: 13px; color: var(--ink-blueprint-3);">This is basic popover content.</p>
        </div>
      </template>
    </Popover>

    <!-- Top placement -->
    <Popover placement="top-start">
      <template #target="{ togglePopover }">
        <Button variant="outline" theme="blueprint" @click="togglePopover">
          Top placement
        </Button>
      </template>
      <template #body>
        <div style="padding: 16px; min-width: 200px;">
          <p style="font-size: 14px; color: var(--ink-blueprint-4);">Opens on top</p>
        </div>
      </template>
    </Popover>

    <!-- Hover trigger -->
    <Popover placement="bottom-start" trigger="hover">
      <template #target>
        <Button variant="subtle" theme="blueprint">
          Hover me
        </Button>
      </template>
      <template #body>
        <div style="padding: 16px; min-width: 200px;">
          <p style="font-size: 14px; color: var(--ink-blueprint-4);">Triggered on hover</p>
        </div>
      </template>
    </Popover>

    <!-- With transition -->
    <Popover placement="bottom-start" transition="default">
      <template #target="{ togglePopover }">
        <Button variant="solid" theme="blueprint" @click="togglePopover">
          With animation
        </Button>
      </template>
      <template #body>
        <div style="padding: 16px; min-width: 200px;">
          <p style="font-size: 14px; color: var(--ink-blueprint-4); margin-bottom: 8px; font-weight: 500;">Animated Popover</p>
          <p style="font-size: 13px; color: var(--ink-blueprint-3); margin-bottom: 12px;">This popover has a fade + slide animation.</p>
          <Button size="sm" variant="solid" theme="blueprint">Action</Button>
        </div>
      </template>
    </Popover>

    <!-- Right placement -->
    <Popover placement="right-start">
      <template #target="{ togglePopover }">
        <Button variant="ghost" theme="blueprint" @click="togglePopover">
          Right placement
        </Button>
      </template>
      <template #body>
        <div style="padding: 16px; min-width: 200px;">
          <p style="font-size: 14px; color: var(--ink-blueprint-4);">Opens on right</p>
        </div>
      </template>
    </Popover>

  </div>
</div>
<!-- List Filter -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">LIST FILTER</p>
  <div style="display: flex; gap: 12px; flex-wrap: wrap; align-items: center;">

    <!-- Empty filters -->
    <ListFilter
      :docfields="docfields"
      v-model="listFilterValue"
    />

  </div>
  <div style="margin-top: 12px; font-size: 12px;">
    Active filters: {{ JSON.stringify(listFilterValue) }}
  </div>
</div>
<!-- Form Control -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">FORM CONTROL</p>
  <div style="display: flex; flex-direction: column; gap: 12px; max-width: 400px;">

    <!-- Text -->
    <FormControl
      type="text"
      size="sm"
      variant="subtle"
      label="Text input"
      placeholder="Enter text"
      description="Helper text below"
      v-model="formControlText"
    />

    <!-- Outline -->
    <FormControl
      type="text"
      size="sm"
      variant="outline"
      label="Outline input"
      placeholder="Enter text"
      v-model="formControlText"
    />

    <!-- Select -->
    <FormControl
      type="select"
      size="sm"
      variant="subtle"
      label="Select"
      placeholder="Select option"
      :options="[
        { label: 'Option 1', value: 'opt1' },
        { label: 'Option 2', value: 'opt2' },
        { label: 'Option 3', value: 'opt3' },
      ]"
      v-model="formControlSelect"
    />

    <!-- Combobox -->
    <FormControl
      type="combobox"
      size="sm"
      variant="subtle"
      label="Combobox"
      placeholder="Search options"
      :options="[
        { label: 'Project Management', value: 'pm' },
        { label: 'Finance', value: 'finance' },
        { label: 'Procurement', value: 'procurement' },
      ]"
      v-model="formControlCombobox"
    />

    <!-- Textarea -->
    <FormControl
      type="textarea"
      size="sm"
      variant="subtle"
      label="Textarea"
      placeholder="Enter description"
      v-model="formControlTextarea"
    />

    <!-- Disabled -->
    <FormControl
      type="text"
      size="sm"
      variant="subtle"
      label="Disabled"
      placeholder="Disabled input"
      :disabled="true"
    />

    <!-- With error -->
    <FormControl
      type="text"
      size="sm"
      variant="subtle"
      label="With error"
      placeholder="Enter value"
      v-model="formControlText"
    />
    <ErrorMessage message="This field is required" />

  </div>
</div>

<!-- Dropdown -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">DROPDOWN</p>
  <div style="display: flex; gap: 16px; flex-wrap: wrap; align-items: center;">

    <!-- Basic -->
    <Dropdown :options="dropdownOptions">
      <Button variant="outline" theme="blueprint">
        Actions
        <template #suffix>
          <span class="lucide-chevron-down size-4" />
        </template>
      </Button>
    </Dropdown>

    <!-- With groups -->
    <Dropdown
      :options="[
        {
          group: 'Actions',
          items: [
            { label: 'Edit', icon: 'edit-2', onClick: () => {} },
            { label: 'Duplicate', icon: 'copy', onClick: () => {} },
          ]
        },
        {
          group: 'Danger',
          items: [
            { label: 'Delete', icon: 'trash-2', theme: 'red', onClick: () => {} },
          ]
        }
      ]"
    >
      <Button variant="subtle" theme="blueprint">
        With groups
        <template #suffix>
          <span class="lucide-chevron-down size-4" />
        </template>
      </Button>
    </Dropdown>

    <!-- Disabled item -->
    <Dropdown
      :options="[
        { label: 'Active option', onClick: () => {} },
        { label: 'Disabled option', disabled: true, onClick: () => {} },
        { label: 'Another option', onClick: () => {} },
      ]"
    >
      <Button variant="ghost" theme="blueprint">
        With disabled
        <template #suffix>
          <span class="lucide-chevron-down size-4" />
        </template>
      </Button>
    </Dropdown>

  </div>
</div>
<!-- Command Palette -->
<div>
  <p style="font-size: 12px; margin-bottom: 12px; color: var(--text-ink-gray-5);">COMMAND PALETTE</p>
  <div style="display: flex; gap: 12px; align-items: center;">
    <Button variant="outline" theme="blueprint" @click="showCommandPalette = true">
      Open Command Palette
      <template #suffix>
        <span style="font-size: 11px; opacity: 0.7;">⌘K</span>
      </template>
    </Button>
    <span style="font-size: 12px; color: var(--ink-blueprint-3);">or press Cmd+K anywhere</span>
  </div>

  <CommandPalette
    v-model:show="showCommandPalette"
    v-model:searchQuery="commandSearch"
    :groups="commandGroups"
    @select="(item) => console.log('Selected:', item)"
  />
</div>
    </div>
  </div>
</template>
