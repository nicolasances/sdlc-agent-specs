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