# Frontend Coding Standards for React

## Building UI Components

### Prefer composition over configuration

```tsx
// Good: Composable
<Card>
  <CardHeader>
    <CardTitle>Tasks</CardTitle>
  </CardHeader>
  <CardBody>
    <TaskList tasks={tasks} />
  </CardBody>
</Card>

// Avoid: Over-configured
<Card
  title="Tasks"
  headerVariant="large"
  bodyPadding="md"
  content={<TaskList tasks={tasks} />}
/>
```

### Keep components focused

```tsx
// Good: Does one thing
export function TaskItem({ task, onToggle, onDelete }: TaskItemProps) {
  return (
    <li className="flex items-center gap-3 p-3">
      <Checkbox checked={task.done} onChange={() => onToggle(task.id)} />
      <span className={task.done ? 'line-through text-muted' : ''}>{task.title}</span>
      <Button variant="ghost" size="sm" onClick={() => onDelete(task.id)}>
        <TrashIcon />
      </Button>
    </li>
  );
}
```

### Keep loading skeletons and error management in the component rather than as a separate component

```tsx
// Good: Skeleton inside component
<ContinueCard module={currentModule ?? null} loading={isProgressLoading} />
<LevelTrack
    cefrLevel={cefrLevel}
    levelName={levelName}
    totalModules={currentLevelSummary.modulesTotal}
    completedModules={currentLevelSummary.modulesCompleted}ù
    loading={isProgressLoading}
    error={!progress || !cefrLevel || !levelName || !currentLevelSummary}
/>

// Avoid: Separate skeleton or error component
{isProgressLoading ? (
    <ContinueCardSkeleton />
) : (
    <ContinueCard module={currentModule ?? null} />
)}
{isProgressLoading ? (
    <LevelTrackSkeleton />
) : progress && cefrLevel && levelName && currentLevelSummary ? (
    <LevelTrack
        cefrLevel={cefrLevel}
        levelName={levelName}
        totalModules={currentLevelSummary.modulesTotal}
        completedModules={currentLevelSummary.modulesCompleted}
    />
) : (
    <LevelTrackError />
)}
```

### Usage of MaskedSvgIcon

**Always** use `<MaskedSvgIcon/>` from `toto-react` when: 
- you need to display a standalone SVG icon

**DO NOT** use `<MaskedSvgIcon/>` from `toto-react` when: 
- you want to display a `<RoundButton />` from `toto-react`: that already uses `<MaskedSvgIcon/>` internally.

**RED Flags:**
- you have created an inline SVG. That should **never** happen.


### Tailwind over custom CSS classes and inline styles

**Always** perfer Tailwind classes over: 
- inline CSS
- custom CSS classes

```typescript
// AVOID this: 
<span
    style={{
        fontSize: 11,
        fontWeight: 600,
        color: 'rgba(0,0,0,0.50)',
        letterSpacing: '0.10em',
        textTransform: 'uppercase',
    }}
>
    Some text
</span>

// Instead PREFER THIS: 
<span className="text-sm font-semibold uppercase tracking-widest text-black/50">
    Some text
</span>
```

### Inline style for component definition 

For readability purposes, I **do not like** components whose definition is split in multiple rows. 
**I like the function definition to be on one row**. 

```typescript
// AVOID this: 
export function ModuleHeader({
    kicker,
    title,
    communicationGoal,
}: {
    kicker: string;
    title: string;
    communicationGoal: string;
})

// Instead PREFER THIS: 
export function ModuleHeader({kicker, title, communicationGoal}: {kicker: string, title: string, communicationGoal: string})
``` 